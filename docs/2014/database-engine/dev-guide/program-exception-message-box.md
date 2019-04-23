---
title: 程式例外狀況訊息方塊 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- exception message box [SQL Server]
- displaying exception message box
ms.assetid: c771985b-149c-459a-b3cb-7b15fde01150
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 316afc6d5f3a87ff7431240681066ac5ee66ede6
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "60157934"
---
# <a name="program-exception-message-box"></a>程式例外狀況訊息方塊
  您可以在應用程式中使用例外狀況訊息方塊，此訊息方塊對訊息經驗所提供的控制要比 <xref:System.Windows.Forms.MessageBox> 類別所提供的高出許多。 如需詳細資訊，請參閱 <<c0> [ 例外狀況訊息方塊程式設計](../../../2014/database-engine/dev-guide/exception-message-box-programming.md)。 如需有關如何取得及部署例外狀況訊息方塊 .dll 的詳細資訊，請參閱＜ [Deploying an Exception Message Box Application](../../../2014/database-engine/dev-guide/deploying-an-exception-message-box-application.md)＞。  
  
## <a name="procedure"></a>程序  
  
#### <a name="to-handle-an-exception-by-using-the-exception-message-box"></a>使用例外狀況訊息方塊處理例外狀況  
  
1.  在 Managed 程式碼專案中加入 Microsoft.ExceptionMessageBox.dll 組件的參考。  
  
2.  （選擇性）新增`using`(C#) 或`Imports`([!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic.NET) 指示詞，以使用<xref:Microsoft.SqlServer.MessageBox>命名空間。  
  
3.  建立 try-catch 區塊來處理預期的例外狀況。  
  
4.  在 `catch` 區塊內建立 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 類別的執行個體。 傳遞<xref:System.Exception>處理物件`try` - `catch`區塊。  
  
5.  (選擇性) 在 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 上設定下列其中一個或多個屬性：  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> 列舉，指定要在例外狀況訊息方塊中顯示的按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> 列舉，指定例外狀況訊息方塊的預設按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> 列舉，用於控制例外狀況訊息方塊的其他行為。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> 列舉，指定要在例外狀況訊息方塊中顯示的符號。  
  
6.  呼叫 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 方法。 傳遞例外狀況訊息方塊所屬的父視窗。  
  
7.  (選擇性) 如需判斷使用者所按的按鈕，請注意傳回的 <xref:System.Windows.Forms.DialogResult> 列舉值。  
  
#### <a name="to-display-the-exception-message-box-without-an-exception"></a>顯示沒有例外狀況的例外狀況訊息方塊  
  
1.  在 Managed 程式碼專案中加入 Microsoft.ExceptionMessageBox.dll 組件的參考。  
  
2.  （選擇性）新增`using`(C#) 或`Imports`(Visual Basic.NET) 指示詞，以使用<xref:Microsoft.SqlServer.MessageBox>命名空間。  
  
3.  建立 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 類別的執行個體。 將訊息文字當做 <xref:System.String> 值傳遞。  
  
4.  (選擇性) 在 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 上設定下列其中一個或多個屬性：  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> 列舉，指定要在例外狀況訊息方塊中顯示的按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Caption%2A> - 例外狀況訊息方塊的對話方塊標題。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> 列舉，指定例外狀況訊息方塊的對話方塊中的 [預設] 按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> 列舉，用於控制例外狀況訊息方塊的其他行為。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> 列舉，指定要在例外狀況訊息方塊中顯示的符號。  
  
5.  呼叫 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 方法。 傳遞例外狀況訊息方塊所屬的父視窗。  
  
6.  (選擇性) 如需判斷使用者所按的按鈕，請注意傳回的 <xref:System.Windows.Forms.DialogResult> 列舉值。  
  
#### <a name="to-display-the-exception-message-box-with-customized-buttons"></a>顯示具有自訂按鈕的例外狀況訊息方塊  
  
1.  在 Managed 程式碼專案中加入 Microsoft.ExceptionMessageBox.dll 組件的參考。  
  
2.  （選擇性）新增`using`(C#) 或`Imports`(Visual Basic.NET) 指示詞，以使用<xref:Microsoft.SqlServer.MessageBox>命名空間。  
  
3.  以下列兩種方式中的一種來建立 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 類別的執行個體：  
  
    -   傳遞<xref:System.Exception>處理物件`try` - `catch`區塊。  
  
    -   將訊息文字當做 <xref:System.String> 值傳遞。  
  
4.  針對 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> 設定下列其中一個值：  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.AbortRetryIgnore> -顯示**中止**，**重試一次**，並**忽略**按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.Custom> - 顯示自訂按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OK> -顯示**確定** 按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OKCancel> -顯示 **[確定]** 並**取消**按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.RetryCancel> -顯示**重試**並**取消**按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNo> -顯示 **[是]** 並**No**按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNoCancel> -顯示 **[是]**， **No**，並**取消**按鈕。  
  
5.  (選擇性) 如果您使用自訂按鈕，請呼叫 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.SetButtonText%2A> 方法的其中一個多載來指定最多五個自訂按鈕的文字。  
  
6.  呼叫 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 方法。 傳遞例外狀況訊息方塊所屬的父視窗。  
  
7.  (選擇性) 如需判斷使用者所按的按鈕，請注意傳回的 <xref:System.Windows.Forms.DialogResult> 列舉值。 如果使用自訂按鈕，請注意 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDialogResult> 屬性的 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CustomDialogResult%2A>，以判斷使用者所按的自訂按鈕。  
  
#### <a name="to-allow-users-to-decide-whether-to-show-the-exception-message-box"></a>讓使用者決定是否顯示例外狀況訊息方塊  
  
1.  在 Managed 程式碼專案中加入 Microsoft.ExceptionMessageBox.dll 組件的參考。  
  
2.  （選擇性）新增`using`(C#) 或`Imports`(Visual Basic.NET) 指示詞，以使用<xref:Microsoft.SqlServer.MessageBox>命名空間。  
  
3.  以下列兩種方式中的一種來建立 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 類別的執行個體：  
  
    -   傳遞<xref:System.Exception>處理物件`try` - `catch`區塊。  
  
    -   將訊息文字當做 <xref:System.String> 值傳遞。  
  
4.  將 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.ShowCheckbox%2A> 屬性設定為 `true`。  
  
5.  (選擇性) 指定文字以要求使用者決定是否針對 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxText%2A> 再次顯示例外狀況訊息方塊。 預設的文字為「不要再顯示此訊息」。  
  
6.  如果只需在應用程式的執行期間保留使用者的決定，請將 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.IsCheckboxChecked%2A> 的值設定為全域的 <xref:System.Boolean> 變數。 在建立例外狀況訊息方塊的執行個體之前，請先評估此值。  
  
7.  如果需要永久儲存使用者的決定，請進行下列步驟：  
  
    1.  呼叫 CreateSubKey 方法來開啟應用程式所使用的自訂登錄機碼，然後將 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryKey%2A> 設定為傳回的 RegistryKey 物件。  
  
    2.  將 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryValue%2A> 設定為所使用之登錄值的名稱。  
  
    3.  將 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryMeansDoNotShowDialog%2A> 設定為 `true`。  
  
    4.  呼叫 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 方法。 系統會評估指定的登錄機碼，只有當登錄機碼所儲存的資料為 0 時，才會顯示例外狀況訊息方塊。 如果對話方塊顯示，而且使用者在按按鈕之前先選取了這個核取方塊，則登錄機碼中的資料會設為 1。  
  
## <a name="example"></a>範例  
 此範例所使用的例外狀況訊息方塊只具有 **[確定]** 按鈕，可顯示應用程式例外狀況的資訊，這些資訊包含處理的例外狀況以及其他的應用程式特定資訊。  
  
 [!code-csharp[HowTo#emb_showOKbutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showokbutton)]  
  
 [!code-vb[HowTo#emb_vb_showOKbutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showokbutton)]  
  
## <a name="example"></a>範例  
 此範例所使用的例外狀況訊息方塊具有 **[是]** 和 **[否]** 按鈕，使用者可從中進行選擇。  
  
 [!code-csharp[HowTo#emb_showYesNobutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showyesnobutton)]  
  
 [!code-vb[HowTo#emb_vb_showYesNobutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showyesnobutton)]  
  
## <a name="example"></a>範例  
 此範例所使用的例外狀況訊息方塊具有自訂按鈕。  
  
 [!code-csharp[HowTo#emb_showcustombutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showcustombutton)]  
  
 [!code-vb[HowTo#emb_vb_showcustombutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showcustombutton)]  
  
## <a name="example"></a>範例  
 此範例使用核取方塊來決定是否顯示例外狀況訊息方塊。  
  
 [!code-csharp[HowTo#emb_usecheckbox](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_usecheckbox)]  
  
 [!code-vb[HowTo#emb_vb_usecheckbox](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_usecheckbox)]  
  
## <a name="example"></a>範例  
 此範例使用核取方塊和登錄機碼來決定是否顯示例外狀況訊息方塊。  
  
 [!code-csharp[HowTo#emb_useregkey](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_useregkey)]  
  
 [!code-vb[HowTo#emb_vb_useregkey](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_useregkey)]  
  
## <a name="example"></a>範例  
 此範例使用例外狀況訊息方塊來顯示額外的資訊，這些資訊在進行疑難排解或偵錯時很有用。  
  
 [!code-csharp[HowTo#emb_moreinfo](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_moreinfo)]  
  
 [!code-vb[HowTo#emb_vb_moreinfo](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_moreinfo)]  
  
  
