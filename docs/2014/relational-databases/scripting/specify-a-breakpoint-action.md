---
title: 指定中斷點動作
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint action
- Transact-SQL debugger, breakpoint when hit action
ms.assetid: f97f0097-6f51-40c1-b2e0-294a93ce1e1b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08df1a4c00bf3b019cf45f168aeeaaf27fdb751c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "75243238"
---
# <a name="specify-a-breakpoint-action"></a>指定中斷點動作
  中斷點 [叫用時]  動作指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具針對中斷點所執行的自訂工作。 如果已到達指定的叫用計數而且滿足任何指定的中斷點條件時，偵錯工具就會執行為中斷點指定的動作。  
  
##  <a name="BKMK_ActionConsiderations"></a> 動作考量因素  
 中斷點的預設動作是在已滿足叫用計數和中斷點條件時中斷執行。 **偵錯工具中 [叫用時]** [!INCLUDE[tsql](../../includes/tsql-md.md)] 動作的主要用法是透過指定列印訊息，將資訊列印至偵錯工具 [輸出]  視窗。  
  
 列印訊息是在 [列印訊息]  選項中指定，並指定為文字字串，其中的運算式包含來自偵錯中 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的資訊。 運算式包含：  
  
-   以大括號 ([!INCLUDE[tsql](../../includes/tsql-md.md)]) 括住的 {} 運算式。 運算式可以包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 變數、參數和內建函數。 範例包括 {@MyVariable}、{@NameParameter}、{@@SPID} 或 {SERVERPROPERTY('ProcessID')}。  
  
-   下列其中一個關鍵字：  
  
    1.  $ADDRESS 傳回設定中斷點之預存程序或使用者定義函數的名稱。 如果中斷點是在編輯器視窗中設定，$ADDRESS 會傳回編輯中指令碼檔案的名稱。 $ADDRESS 和 $FUNCTION 會在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具中傳回相同資訊。  
  
    2.  $CALLER 傳回呼叫預存程序或函數之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼單元的名稱。 如果中斷點是在編輯器視窗中設定，$CALLER 會傳回 \<沒有可用的呼叫端>。 如果中斷點是在編輯器視窗中程式碼所呼叫的預存程序或使用者定義函數中，$CALLER 會傳回編輯中檔案的名稱。 如果中斷點是在另一個預存程序或函數所呼叫的預存程序或使用者定義函數中，$CALLER 會傳回呼叫程序或函數的名稱。  
  
    3.  $CALLSTACK 傳回鏈結中呼叫目前預存程序或使用者定義函數之函數的呼叫堆疊。 如果中斷點是在編輯器視窗中，$CALLSTACK 會傳回編輯中指令碼檔案的名稱。  
  
    4.  $FUNCTION 傳回設定中斷點之預存程序或使用者定義函數的名稱。 如果中斷點是在編輯器視窗中設定，$FUNCTION 會傳回編輯中指令碼檔案的名稱。  
  
    5.  $PID 與 $PNAME 會傳回執行 Database Engine 執行個體且執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 之作業系統處理序的識別碼及名稱。 $PID 和 SERVERPROPERTY('ProcessID') 傳回相同的識別碼，不同之處在於 $PID 是十六進位值，而 SERVERPROPERTY('ProcessID') 是十進位值。  
  
    6.  $TID 與 $TNAME 會傳回執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次之作業系統執行緒的識別碼及名稱。 執行緒與執行 Database Engine 執行個體的處理序相關聯。 $TID 與 SELECT kpid FROM sys.sysprocesses WHERE spid = @@SPID 傳回相同的值，不同之處在於 $TID 是十六進位值，而 kpid 是十進位值。  
  
-   您也可以使用反斜線字元 (\\) 當做逸出字元，允許在訊息中使用大括號和反斜線： \\{、 \\} 和 \\\\。  
  
#### <a name="to-specify-a-when-hit-action"></a>若要指定叫用時動作  
  
1.  在編輯器視窗中，以滑鼠右鍵按一下中斷點字符，然後按一下捷徑功能表上的 [叫用時]  。  
  
     -或-  
  
     在 [中斷點]  視窗中，以滑鼠右鍵按一下中斷點字符，然後按一下捷徑功能表上的 [叫用時]  。  
  
2.  在 [叫用中斷點時]  對話方塊中，選取所要的行為：  
  
    1.  選取 [列印訊息]  ，以便在叫用中斷點時，在偵錯工具的 [輸出] 視窗中列印訊息。  
  
    2.  [執行巨集]  選項無法在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具中使用，會呈現灰色。  
  
    3.  如果不要讓中斷點暫停執行，請選取 [繼續執行]  。 只有當您選取了 [列印訊息]  選項時，才能使用這個選項。  
  
3.  按一下 **[確定]** 實作變更，或按一下 **[取消]** 結束而不套用變更。  
  
## <a name="see-also"></a>另請參閱  
 [指定中斷點條件](specify-a-breakpoint-condition.md)   
 [指定叫用計數](specify-a-hit-count.md)  
