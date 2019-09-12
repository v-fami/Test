# <a name="bug-check-0x1e-kmode_exception_not_handled"></a><span data-ttu-id="06e38-106">Bug 检查 0x1E：\_未\_处理KMODE\_异常</span><span class="sxs-lookup"><span data-stu-id="06e38-106">Bug Check 0x1E: KMODE\_EXCEPTION\_NOT\_HANDLED</span></span>


<span data-ttu-id="06e38-107">未\_\_处理的KMODE异常bug检查的值为0x0000001e。\_</span><span class="sxs-lookup"><span data-stu-id="06e38-107">The KMODE\_EXCEPTION\_NOT\_HANDLED bug check has a value of 0x0000001E.</span></span> <span data-ttu-id="06e38-108">这表示内核模式程序生成了错误处理程序未捕获的异常。</span><span class="sxs-lookup"><span data-stu-id="06e38-108">This indicates that a kernel-mode program generated an exception which the error handler did not catch.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06e38-109">本主题面向程序员。</span><span class="sxs-lookup"><span data-stu-id="06e38-109">This topic is for programmers.</span></span> <span data-ttu-id="06e38-110">如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。</span><span class="sxs-lookup"><span data-stu-id="06e38-110">If you are a customer who has received a blue screen error code while using your computer, see [Troubleshoot blue screen errors](https://www.windows.com/stopcode).</span></span>


## <a name="kmode_exception_not_handled-parameters"></a><span data-ttu-id="06e38-111">KMODE\_异常\_未\_处理的参数</span><span class="sxs-lookup"><span data-stu-id="06e38-111">KMODE\_EXCEPTION\_NOT\_HANDLED Parameters</span></span>


<table><span data-ttu-id="06e38-112">  
<colgroup>  
<col width="50%" />  
<col width="50%" />  
</colgroup>  
<thead>  
<tr class="header">  
<th align="left">参数</span><span class="sxs-lookup"><span data-stu-id="06e38-112">  
<colgroup>  
<col width="50%" />  
<col width="50%" />  
</colgroup>  
<thead>  
<tr class="header">  
<th align="left">Parameter</span></span></th>
<th align="left"><span data-ttu-id="06e38-113">描述</span><span class="sxs-lookup"><span data-stu-id="06e38-113">Description</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span data-ttu-id="06e38-114">1</span><span class="sxs-lookup"><span data-stu-id="06e38-114">1</span></span></p></td>
<td align="left"><p><span data-ttu-id="06e38-115">未处理的异常代码</span><span class="sxs-lookup"><span data-stu-id="06e38-115">The exception code that was not handled</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><p><span data-ttu-id="06e38-116">2</span><span class="sxs-lookup"><span data-stu-id="06e38-116">2</span></span></p></td>
<td align="left"><p><span data-ttu-id="06e38-117">发生异常的地址</span><span class="sxs-lookup"><span data-stu-id="06e38-117">The address at which the exception occurred</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span data-ttu-id="06e38-118">3</span><span class="sxs-lookup"><span data-stu-id="06e38-118">3</span></span></p></td>
<td align="left"><p><span data-ttu-id="06e38-119">异常的参数0</span><span class="sxs-lookup"><span data-stu-id="06e38-119">Parameter 0 of the exception</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><p><span data-ttu-id="06e38-120">4</span><span class="sxs-lookup"><span data-stu-id="06e38-120">4</span></span></p></td>
<td align="left"><p><span data-ttu-id="06e38-121">异常的参数1</span><span class="sxs-lookup"><span data-stu-id="06e38-121">Parameter 1 of the exception</span></span></p></td>
</tr>
</tbody>
</table>
