---
title: 程式例外狀況訊息方塊 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- exception message box [SQL Server]
- displaying exception message box
ms.assetid: c771985b-149c-459a-b3cb-7b15fde01150
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a6d5e6112822b1191894c633b89f8b2d54b95e6f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030863"
---
# <a name="program-exception-message-box"></a>程式例外狀況訊息方塊
  您可以在應用程式中使用例外狀況訊息方塊，以提供更有效地控制訊息經驗所提供比<xref:System.Windows.Forms.MessageBox>類別。 如需詳細資訊，請參閱[例外狀況訊息方塊程式設計](../../../2014/database-engine/dev-guide/exception-message-box-programming.md)。 如需如何取得及部署例外狀況訊息方塊.dll 的資訊，請參閱[例外狀況訊息方塊應用程式部署到](../../../2014/database-engine/dev-guide/deploying-an-exception-message-box-application.md)。  
  
## <a name="procedure"></a>程序  
  
#### <a name="to-handle-an-exception-by-using-the-exception-message-box"></a>使用例外狀況訊息方塊處理例外狀況  
  
1.  在 Managed 程式碼專案中加入 Microsoft.ExceptionMessageBox.dll 組件的參考。  
  
2.  （選擇性）新增`using`(C#) 或`Imports`([!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic.NET) 指示詞，以使用<xref:Microsoft.SqlServer.MessageBox>命名空間。  
  
3.  建立 try-catch 區塊來處理預期的例外狀況。  
  
4.  內`catch`封鎖，請建立的執行個體<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>類別。 傳遞<xref:System.Exception>物件由`try` - `catch`區塊。  
  
5.  （選擇性）設定一或多個下列屬性<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> 列舉，指定要在例外狀況訊息方塊中顯示的按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> 列舉，指定例外狀況訊息方塊的預設按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> 列舉，用於控制例外狀況訊息方塊的其他行為。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> 列舉，指定要在例外狀況訊息方塊中顯示的符號。  
  
6.  呼叫 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 方法。 傳遞例外狀況訊息方塊所屬的父視窗。  
  
7.  （選擇性）記下的值傳回<xref:System.Windows.Forms.DialogResult>列舉型別，如果您需要決定的按鈕使用者按下。  
  
#### <a name="to-display-the-exception-message-box-without-an-exception"></a>顯示沒有例外狀況的例外狀況訊息方塊  
  
1.  在 Managed 程式碼專案中加入 Microsoft.ExceptionMessageBox.dll 組件的參考。  
  
2.  （選擇性）新增`using`(C#) 或`Imports`(Visual Basic.NET) 指示詞，以使用<xref:Microsoft.SqlServer.MessageBox>命名空間。  
  
3.  建立 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 類別的執行個體。 傳遞訊息文字當做<xref:System.String>值。  
  
4.  （選擇性）設定一或多個下列屬性<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> 列舉，指定要在例外狀況訊息方塊中顯示的按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Caption%2A> - 例外狀況訊息方塊的對話方塊標題。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> 列舉，指定例外狀況訊息方塊的對話方塊的預設按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> 列舉，用於控制例外狀況訊息方塊的其他行為。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> 列舉，指定要在例外狀況訊息方塊中顯示的符號。  
  
5.  呼叫 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 方法。 傳遞例外狀況訊息方塊所屬的父視窗。  
  
6.  （選擇性）請注意傳回的值<xref:System.Windows.Forms.DialogResult>列舉型別，如果您需要決定的按鈕使用者按下。  
  
#### <a name="to-display-the-exception-message-box-with-customized-buttons"></a>顯示具有自訂按鈕的例外狀況訊息方塊  
  
1.  在 Managed 程式碼專案中加入 Microsoft.ExceptionMessageBox.dll 組件的參考。  
  
2.  （選擇性）新增`using`(C#) 或`Imports`(Visual Basic.NET) 指示詞，以使用<xref:Microsoft.SqlServer.MessageBox>命名空間。  
  
3.  以下列兩種方式中的一種來建立 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 類別的執行個體：  
  
    -   傳遞<xref:System.Exception>物件由`try` - `catch`區塊。  
  
    -   傳遞訊息文字當做<xref:System.String>值。  
  
4.  設定下列其中一個值<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.AbortRetryIgnore> -顯示**中止**，**重試**，和**忽略**按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.Custom> -顯示自訂按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OK> -顯示**確定** 按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OKCancel> -顯示**確定**和**取消**按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.RetryCancel> -顯示**重試**和**取消**按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNo> -顯示**是**和**否**按鈕。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNoCancel> -顯示**是**，**否**，和**取消**按鈕。  
  
5.  （選擇性）如果您使用自訂按鈕時，呼叫其中一個多載的<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.SetButtonText%2A>方法，以指定最多五個自訂按鈕的文字。  
  
6.  呼叫 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 方法。 傳遞例外狀況訊息方塊所屬的父視窗。  
  
7.  （選擇性）請注意傳回的值<xref:System.Windows.Forms.DialogResult>列舉型別，如果您需要決定的按鈕使用者按下。 如果您使用自訂按鈕時，請注意值<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDialogResult>如<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CustomDialogResult%2A>屬性來判斷您的自訂按鈕，使用者按下。  
  
#### <a name="to-allow-users-to-decide-whether-to-show-the-exception-message-box"></a>讓使用者決定是否顯示例外狀況訊息方塊  
  
1.  在 Managed 程式碼專案中加入 Microsoft.ExceptionMessageBox.dll 組件的參考。  
  
2.  （選擇性）新增`using`(C#) 或`Imports`(Visual Basic.NET) 指示詞，以使用<xref:Microsoft.SqlServer.MessageBox>命名空間。  
  
3.  以下列兩種方式中的一種來建立 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 類別的執行個體：  
  
    -   傳遞<xref:System.Exception>物件由`try` - `catch`區塊。  
  
    -   傳遞訊息文字當做<xref:System.String>值。  
  
4.  設定<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.ShowCheckbox%2A>屬性`true`。  
  
5.  （選擇性）指定文字以要求使用者決定是否顯示例外狀況訊息方塊，再為<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxText%2A>。 預設的文字為「不要再顯示此訊息」。  
  
6.  如果您需要保留使用者的決策，只會針對應用程式的執行期間，設定的值<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.IsCheckboxChecked%2A>全域<xref:System.Boolean>變數。 在建立例外狀況訊息方塊的執行個體之前，請先評估此值。  
  
7.  如果需要永久儲存使用者的決定，請進行下列步驟：  
  
    1.  呼叫 CreateSubKey 方法來開啟應用程式所使用的自訂登錄機碼，並設定<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryKey%2A>傳回的 RegistryKey 物件。  
  
    2.  將 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryValue%2A> 設定為所使用之登錄值的名稱。  
  
    3.  設定<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryMeansDoNotShowDialog%2A>至`true`。  
  
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
  
  