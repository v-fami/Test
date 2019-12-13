# <a name="configure-a-virtual-machine-with-desired-state-configuration"></a>필요한 상태 구성을 사용하여 가상 머신 구성

DSC(Desired State Configuration)를 사용하면 Windows 및 Linux 서버의 구성을 관리하고 모니터링할 수 있습니다. 필요한 구성에서 벗어나는 구성을 식별하거나 자동으로 수정할 수 있습니다. 이 빠른 시작에서는 Linux VM을 등록하고 DSC로 LAMP 스택을 배포하는 방법을 안내합니다.

## <a name="prerequisites"></a>필수 조건

이 빠른 시작을 완료하려면 다음이 필요합니다.

* Azure 구독. Azure 구독이 아직 없는 경우 [무료 계정을 만듭니다](https://azure.microsoft.com/free/).
* Azure Automation 계정. Azure Automation 실행 계정 만들기에 대한 지침은 [Azure 실행 계정](automation-sec-configure-azure-runas-account.md)을 참조하세요.
* Red Hat Enterprise Linux, CentOS 또는 Oracle Linux를 실행하는 Azure Resource Manager VM(클래식이 아님). VM 만들기에 대한 지침은 [Azure Portal에서 Linux 가상 머신 만들기](../virtual-machines/linux/quick-create-portal.md)를 참조하세요.

## <a name="sign-in-to-azure"></a>Azure에 로그인
 https://portal.azure.com 에서 Azure에 로그인

## <a name="onboard-a-virtual-machine"></a>가상 머신 등록
여러 가지 방법으로 컴퓨터를 등록하고 DSC를 사용하도록 설정할 수 있습니다. 이 빠른 시작에서는 Automation 계정을 통한 등록에 대해 설명합니다. [등록](https://docs.microsoft.com/azure/automation/automation-dsc-onboarding) 문서를 참조하여 컴퓨터를 DSC에 등록하는 방법에 대해 자세히 알아볼 수 있습니다.
