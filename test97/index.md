---
ms.openlocfilehash: a294989867bc3849710f16ac1bc0a8c6f8e1903a
ms.sourcegitcommit: b4e206ccfeb7e0f628c237a2c823763c4e2b5e56
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/14/2019
ms.locfileid: "73170482"
---
이제 NVA(네트워크 가상 어플라이언스)와 가상 머신을 만들었으므로, NVA를 통해 트래픽을 라우팅합니다.

![가상 머신 및 IP 주소](../media/6-vms-ip-addresses.svg)

## <a name="create-public-and-private-virtual-machines"></a>퍼블릭 및 프라이빗 가상 머신 만들기

다음 단계는 퍼블릭 및 프라이빗 서브넷에 가상 머신을 배포하는 것입니다.

1. Visual Studio Code 편집기를 열고 cloud-init.txt라는 파일을 만듭니다.

    ```bash
    code cloud-init.txt
    ```

1. 다음 구성 정보를 파일에 추가합니다. 이 구성을 사용하여 `inetutils-traceroute` 패키지는 새 가상 머신을 만들 때 설치됩니다. 이 패키지에는 이 연습의 뒷부분에서 사용할 `traceroute` 유틸리티가 포함되어 있습니다.

    ```Text
    #cloud-config
    package_upgrade: true
    packages:
       - inetutils-traceroute
    ```

1. 파일을 저장하려면 Ctrl+S를 선택한 다음 편집기를 닫으려면 Ctrl+Q를 선택합니다.

1. Cloud Shell에서 다음 명령을 실행하여 **퍼블릭** 가상 머신을 만듭니다. `<password>`를 **azureuser** 계정에 적합한 암호로 바꿉니다.

    ```azurecli
    az vm create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name public \
        --vnet-name vnet \
        --subnet publicsubnet \
        --image UbuntuLTS \
        --admin-username azureuser \
        --no-wait \
        --custom-data cloud-init.txt \
        --admin-password <password>
    ```

1. 다음 명령을 실행하여 ‘**프라이빗**' 가상 머신을 만듭니다. `<password>`를 적절한 암호로 바꿉니다.

    ```azurecli
    az vm create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name private \
        --vnet-name vnet \
        --subnet privatesubnet \
        --image UbuntuLTS \
        --admin-username azureuser \
        --no-wait \
        --custom-data cloud-init.txt \
        --admin-password <password>
    ```

1. 다음 Linux `watch` 명령을 실행하여 가상 머신이 실행되고 있는지 확인합니다. `watch` 명령은 정기적으로 `az vm list` 명령을 실행하여 가상 머신의 진행률을 모니터링할 수 있습니다.

    ```bash
    watch -d -n 5 "az vm list \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --show-details \
        --query '[*].{Name:name, ProvisioningState:provisioningState, PowerState:powerState}' \
        --output table"
    ```

    **ProvisioningState**가 “성공”이고 **PowerState**가 “VM 실행 중”이면 배포에 성공했음을 나타냅니다. 세 개의 가상 머신이 모두 실행 중이면 다음 단계를 진행해도 됩니다. Ctrl-C를 눌러 명령을 중지하고 연습을 계속 진행합니다.

1. 다음 명령을 실행하여 **퍼블릭** 가상 머신의 공용 IP 주소를 `PUBLICIP`이라는 변수에 저장합니다.

    ```azurecli
    PUBLICIP="$(az vm list-ip-addresses \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name public \
        --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
        --output tsv)"

    echo $PUBLICIP
    ```

1. 다음 명령을 실행하여 ‘프라이빗’ 가상 머신의 퍼블릭 IP 주소를 `PRIVATEIP` 변수에 저장합니다. ****

    ```azurecli
    PRIVATEIP="$(az vm list-ip-addresses \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name private \
        --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
        --output tsv)"

    echo $PRIVATEIP
    ```

## <a name="test-traffic-routing-through-the-network-virtual-appliance"></a>네트워크 가상 어플라이언스를 통한 트래픽 라우팅 테스트

최종 단계에서는 Linux `traceroute` 유틸리티를 사용하여 트래픽이 라우팅되는 방식을 보여줍니다. `ssh` 명령을 사용하여 각 가상 머신에서 `traceroute`를 실행합니다. 첫 번째 테스트는 **퍼블릭** 가상 머신에서 **프라이빗** 가상 머신으로 전송된 ICMP 패킷에서 사용하는 경로를 보여줍니다. 두 번째 테스트는 ‘프라이빗’ 가상 머신에서 ‘퍼블릭' 가상 머신으로 전송된 ICMP 패킷에서 사용하는 경로를 보여 줍니다.********

1. 다음 명령을 실행하여 **퍼블릭**에서 **프라이빗**으로의 경로를 추적합니다. 메시지가 표시되면 앞에서 지정한 **azureuser** 계정의 암호를 입력합니다.

    ```bash
    ssh -t -o StrictHostKeyChecking=no azureuser@$PUBLICIP 'traceroute private --type=icmp; exit'
    ```

    `bash: traceroute: command not found`라는 오류 메시지를 받으면 잠시 기다린 후 명령을 다시 시도합니다. 가상 머신을 배포한 후에 `traceroute`가 자동으로 설치되는 데 1~2분이 걸릴 수 있습니다. 명령이 성공한 후 출력은 다음 예제와 유사하게 표시됩니다.

    ```Text
    traceroute to private.kzffavtrkpeulburui2lgywxwg.gx.internal.cloudapp.net (10.0.1.4), 64 hops max
    1   10.0.2.4  0.710ms  0.410ms  0.536ms
    2   10.0.1.4  0.966ms  0.981ms  1.268ms
    Connection to 52.165.151.216 closed.
    ```

    첫 번째 홉은 10.0.2.4입니다. 이 주소는 **nva**의 프라이빗 IP 주소입니다. 두 번째 홉은 **프라이빗**의 주소, 10.0.1.4입니다. 첫 번째 연습에서는 이 경로를 경로 테이블에 추가하고, 해당 테이블을 ‘publicsubnet’ 서브넷에 연결했습니다.**** 따라서 **퍼블릭**에서 **프라이빗**으로 전송된 모든 트래픽은 네트워크 가상 어플라이언스를 통해 라우팅됩니다.

   ![퍼블릭에서 프라이빗으로 라우팅](../media/6-public-private-route.svg)

1. 다음 명령을 실행하여 **프라이빗**에서 **퍼블릭**으로의 경로를 추적합니다. 메시지가 표시되면 **azureuser** 계정의 암호를 입력합니다.

    ```bash
    ssh -t -o StrictHostKeyChecking=no azureuser@$PRIVATEIP 'traceroute public --type=icmp; exit'
    ```

    다음 명령 출력에서와 같이 트래픽이 NVA를 통하지 않고 **퍼블릭**(10.0.0.4)으로 직접 이동하는 것을 확인할 수 있습니다.

    ```Text
    traceroute to public.kzffavtrkpeulburui2lgywxwg.gx.internal.cloudapp.net (10.0.0.4), 64 hops max
    1   10.0.0.4  1.095ms  1.610ms  0.812ms
    Connection to 52.173.21.188 closed.
    ```

    **프라이빗** 가상 머신은 기본 경로를 사용하고 있으며, 트래픽이 서브넷 간에 직접 라우팅됩니다.

   ![프라이빗에서 퍼블릭으로 라우팅](../media/6-private-public-route.svg)

이제 퍼블릭 인터넷의 트래픽이 프라이빗 서브넷에 도달하기 전에 **dmzsubnet** 서브넷을 통과하도록 서브넷 간의 라우팅을 구성했습니다. **dmzsubnet** 서브넷에 NVA 역할을 수행하는 가상 머신을 추가했습니다. 잠재적인 악성 요청을 탐지하고 의도한 대상에 도달하기 전에 차단하는 논리를 이 NVA에 구현할 수 있습니다.
