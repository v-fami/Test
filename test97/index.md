---
title: 형식과 일치하도록 파일 이름 바꾸기
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 5b7a42a174fecd078e804f2ab3c35fbe442364a6
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594398"
---
# <a name="sync-a-type-to-a-filename-or-a-filename-to-a-type-refactoring"></a><span data-ttu-id="518bf-102">형식을 파일 이름에 동기화 또는 파일 이름을 형식 리팩터링에 동기화</span><span class="sxs-lookup"><span data-stu-id="518bf-102">Sync a type to a filename, or a filename to a type refactoring</span></span>

<span data-ttu-id="518bf-103">이 리팩터링은 다음에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-103">This refactoring applies to:</span></span>

- <span data-ttu-id="518bf-104">C#</span><span class="sxs-lookup"><span data-stu-id="518bf-104">C#</span></span>

- <span data-ttu-id="518bf-105">Visual Basic</span><span class="sxs-lookup"><span data-stu-id="518bf-105">Visual Basic</span></span>

<span data-ttu-id="518bf-106">**내용:** 파일 이름과 일치하도록 형식 이름을 바꾸거나 포함된 형식과 일치하도록 파일 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-106">**What:** Lets you rename a type to match the filename, or rename a filename to match the type it contains.</span></span>

<span data-ttu-id="518bf-107">**시기:** 파일 또는 형식의 이름이 바뀌었지만 일치시킬 해당 파일 또는 형식이 업데이트되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-107">**When:** You have renamed a file or type and haven't yet updated the corresponding file or type to match.</span></span>

<span data-ttu-id="518bf-108">**이유:** 다른 이름의 파일로 형식을 저장하거나 그 반대로 저장하면 검색할 대상을 찾기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-108">**Why:** Placing a type in a file with a different name, or vice-versa, it difficult to find what you're looking for.</span></span> <span data-ttu-id="518bf-109">형식 또는 파일의 이름을 바꾸면 코드를 더 쉽게 읽고 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-109">By renaming either the type or filename, code becomes more readable and easier to navigate.</span></span>

> [!NOTE]
> <span data-ttu-id="518bf-110">이 리팩터링은 .NET Standard 및 .NET Core 프로젝트에서 아직 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-110">This refactoring is not yet available for .NET Standard and .NET Core projects.</span></span>

## <a name="how-to"></a><span data-ttu-id="518bf-111">방법</span><span class="sxs-lookup"><span data-stu-id="518bf-111">How-to</span></span>

1. <span data-ttu-id="518bf-112">동기화할 형식 이름을 강조 표시하거나 형식 이름 내부에 텍스트 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-112">Highlight or place the text cursor inside the name of the type to synchronize:</span></span>

   - <span data-ttu-id="518bf-113">C#:</span><span class="sxs-lookup"><span data-stu-id="518bf-113">C#:</span></span>

       ![강조 표시된 코드 - C#](media/synctype-highlight-cs.png)

   - <span data-ttu-id="518bf-115">Visual Basic:</span><span class="sxs-lookup"><span data-stu-id="518bf-115">Visual Basic:</span></span>

       ![강조 표시된 코드 - Visual Basic](media/synctype-highlight-vb.png)

2. <span data-ttu-id="518bf-117">다음 작업 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-117">Next, do one of the following:</span></span>

   - <span data-ttu-id="518bf-118">**키보드**</span><span class="sxs-lookup"><span data-stu-id="518bf-118">**Keyboard**</span></span>
      - <span data-ttu-id="518bf-119">줄의 임의 위치에서 **Ctrl**+ **.** 를 눌러</span><span class="sxs-lookup"><span data-stu-id="518bf-119">Press **Ctrl**+**.**</span></span> <span data-ttu-id="518bf-120">트리거에 **빠른 작업 및 리팩터링** 메뉴를 선택 **로 파일 이름 바꾸기 *TypeName*.cs** 미리 보기 창 팝업에서 위치 *TypeName* 은 선택한 형식의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-120">to trigger the **Quick Actions and Refactorings** menu and select **Rename file to *TypeName*.cs** from the Preview window popup, where *TypeName* is the name of the type you have selected.</span></span>
      - <span data-ttu-id="518bf-121">줄의 임의 위치에서 **Ctrl**+ **.** 를 눌러</span><span class="sxs-lookup"><span data-stu-id="518bf-121">Press **Ctrl**+**.**</span></span> <span data-ttu-id="518bf-122">**빠른 작업 및 리팩터링** 메뉴를 트리거하고 [미리 보기] 창 팝업에서 **_Filename_으로 형식 이름 바꾸기**를 선택합니다. 여기서 *Filename*은 현재 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-122">to trigger the **Quick Actions and Refactorings** menu and select **Rename type to _Filename_** from the Preview window popup, where *Filename* is the name of the current file.</span></span>
   - <span data-ttu-id="518bf-123">**마우스**</span><span class="sxs-lookup"><span data-stu-id="518bf-123">**Mouse**</span></span>
      - <span data-ttu-id="518bf-124">코드를 마우스 오른쪽 단추로 클릭하고, **빠른 작업 및 리팩터링** 메뉴를 선택하고, [미리 보기] 창 팝업에서  ***TypeName*.cs로 파일 이름 바꾸기**를 선택합니다. 여기서 *TypeName*은 선택한 형식의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-124">Right-click the code, select the **Quick Actions and Refactorings** menu, and select **Rename file to *TypeName*.cs** from the Preview window popup, where *TypeName* is the name of the type you have selected.</span></span>
      - <span data-ttu-id="518bf-125">코드를 마우스 오른쪽 단추로 클릭하고, **빠른 작업 및 리팩터링** 메뉴를 선택하고, [미리 보기] 창 팝업에서  **_Filename_으로 형식 이름 바꾸기**를 선택합니다. 여기서 *Filename*은 현재 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-125">Right-click the code, select the **Quick Actions and Refactorings** menu, and select **Rename type to _Filename_** from the Preview window popup, where *Filename* is the name of the current file.</span></span>

   <span data-ttu-id="518bf-126">형식 또는 파일의 이름이 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-126">The type or file is renamed.</span></span>

   - <span data-ttu-id="518bf-127">C#:  아래 예제에서는 **MyClass.cs** 파일의 이름이 형식 이름과 일치하도록 **MyNewClass.cs**로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-127">C#: In the example below, the file **MyClass.cs** was renamed to **MyNewClass.cs** to match the type name.</span></span>

       ![인라인 결과 C#](media/synctype-result-cs.png)

   - <span data-ttu-id="518bf-129">Visual Basic: 아래 예제에서는 **Employee.vb** 파일의 이름이 형식 이름과 일치하도록 **Person.vb**로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="518bf-129">Visual Basic: In the example below, the file **Employee.vb** was renamed to **Person.vb** to match the type name.</span></span>

       ![인라인 결과 Visual Basic](media/synctype-result-vb.png)

## <a name="see-also"></a><span data-ttu-id="518bf-131">참조</span><span class="sxs-lookup"><span data-stu-id="518bf-131">See also</span></span>

- [<span data-ttu-id="518bf-132">리팩터링</span><span class="sxs-lookup"><span data-stu-id="518bf-132">Refactoring</span></span>](../refactoring-in-visual-studio.md)
