---
title: 자습서 - RBAC 및 Azure Portal을 사용하여 Azure 리소스에 대한 사용자 액세스 권한 부여
description: 이 자습서에서는 Azure Portal에서 RBAC(역할 기반 액세스 제어)를 사용하여 Azure 리소스에 대한 사용자 액세스 권한을 부여하는 방법을 알아봅니다.
services: role-based-access-control
documentationCenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: role-based-access-control
ms.devlang: ''
ms.topic: tutorial
ms.tgt_pltfrm: ''
ms.workload: identity
ms.date: 02/22/2019
ms.author: rolyon
ms.openlocfilehash: f4dd3995df2a068824c4aa6bccca5606d250a165
ms.sourcegitcommit: 4c831e768bb43e232de9738b363063590faa0472
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2019
ms.locfileid: "74419654"
---
# <a name="tutorial-grant-a-user-access-to-azure-resources-using-rbac-and-the-azure-portal"></a>자습서: RBAC 및 Azure Portal을 사용하여 Azure 리소스에 대한 사용자 액세스 권한 부여

[RBAC(역할 기반 액세스 제어)](overview.md)는 Azure 리소스에 대한 액세스를 관리하는 방법입니다. 이 자습서에서는 리소스 그룹에서 가상 머신을 만들고 관리할 수 있는 액세스 권한을 사용자에게 부여합니다.

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * 리소스 그룹 범위에 속한 사용자에게 액세스 권한 부여
> * 액세스 권한 제거

Azure 구독이 아직 없는 경우 시작하기 전에 [체험 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.

## <a name="sign-in-to-azure"></a>Azure에 로그인
 
https://portal.azure.com 에서 Azure Portal에 로그인합니다.

## <a name="create-a-resource-group"></a>리소스 그룹 만들기
