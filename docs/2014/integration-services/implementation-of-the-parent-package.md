---
title: 父封裝的實作 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- parent packages [Integration Services]
ms.assetid: d8f94830-fa27-4151-88df-cbdc6bf0fc80
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2cec1f30ba728f1cf3b808acb2fb362e21d259a4
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058160"
---
# <a name="implementation-of-the-parent-package"></a>父封裝的實作
  設定跨越各種伺服器之 SSIS 封裝的負載平衡時，在完成建立、部署子封裝，以及建立執行這些子封裝的遠端 SQL Server Agent 作業之後，下一個步驟就是建立父封裝。 父封裝將包含許多「執行 SQL Server Agent 作業」工作，每一項工作負責呼叫執行其中一個子封裝的不同 SQL Server Agent 作業。 接著父封裝中的「執行 SQL Server Agent 作業」工作會執行各種 SQL Server Agent 作業。 父封裝中的每項工作都包含如何連接到遠端伺服器以及要在該伺服器上執行哪一項作業之類的資訊。 如需詳細資訊，請參閱 [Execute SQL Server Agent Job Task](control-flow/execute-sql-server-agent-job-task.md)。  
  
 若要識別執行子封裝的父封裝，請在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，以滑鼠右鍵按一下 [方案總管] 中的封裝，然後按一下 **[進入點封裝]**。  
  
## <a name="listing-child-packages"></a>列出子封裝  
 若您將包含父封裝及子封裝的專案部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器，可以檢視由父封裝執行的子封裝清單。 當您執行父封裝時，會在 **中自動產生父封裝的 [概觀]**[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]報告。 該告會列出父封裝中包含的執行封裝工作所執行之子封裝清單，如下圖所示。  
  
 ![含有子套件清單的概觀報表](media/overviewreport-childpackagelisting.png "含有子套件清單的概觀報表")  
  
 如需存取 [概觀]  報告的資訊，請參閱＜ [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md)＞。  
  
## <a name="precedence-constraints-in-the-parent-package"></a>父封裝中的優先順序條件約束  
 建立父封裝中「執行 SQL Server Agent 作業」工作之間的優先順序條件約束時，這些優先順序條件約束只會控制遠端伺服器上 SQL Server Agent 作業的啟動時間。 優先順序條件約束不會接收有關從 SQL Server Agent 作業步驟執行之子封裝成功或失敗的資訊。  
  
 這表示子封裝的成功與否並不會傳播至父封裝，因為父封裝中「執行 SQL Server Agent」作業的唯一功能是要求 SQL Server Agent 作業執行子封裝。 在成功呼叫 SQL Server Agent 作業之後，父封裝將會收到 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success> 的結果。  
  
 這種狀況下的失敗只代表呼叫遠端「SQL Server Agent 作業」工作的失敗。 可能發生這種錯誤的其中一種情況是遠端伺服器已經關閉而且代理程式無法回應。 不過，只要代理程式有反應，就代表父封裝已經順利完成其工作。  
  
> [!NOTE]  
>  您可以使用包含 Transact-SQL 陳述式為 **sp_start_job N'package_name'** 的「執行 SQL 工作」。 如需詳細資訊，請參閱 [sp_start_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql)。  
  
## <a name="debugging-environment"></a>環境偵錯  
 測試父封裝時，請使用 [偵錯] / [開始偵錯] (F5) 來執行以使用設計師的偵錯環境。 或者，也可以使用命令提示公用程式 **dtexec**。 如需詳細資訊，請參閱 [dtexec Utility](packages/dtexec-utility.md)。  
  
  
