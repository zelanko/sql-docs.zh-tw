---
title: 新增 Transact-SQL 程式碼片段 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 901c7995-8eb5-4d12-8bb0-de0a922b48f8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b93171cad6896b32086604b54bce30c3fe396fb5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48144318"
---
# <a name="add-transact-sql-snippets"></a>新增 Transact-SQL 程式碼片段
  將您自己的 Transact-SQL 程式碼片段加入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中包含的預先定義程式碼片段集合。  
  
## <a name="creating-a-transact-sql-snippet-file"></a>建立 Transact-SQL 程式碼片段檔案  
 建立 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼片段的第一部分是使用您自己的程式碼片段文字建立 XML 檔案。 此檔案必須有 .snippet 副檔名，且必須符合 [程式碼片段結構描述參考](http://go.microsoft.com/fwlink/?LinkId=207504)的需求。 將程式碼片段語言設定為 SQL。  
  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所隨附的預先定義程式碼片段當做範例。 若要尋找預先定義的程式碼片段，請開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，選取 [工具] 功能表，然後按一下 [程式碼片段管理員]。 在 **[語言]** 清單方塊中選取 **[SQL]** ， [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼片段的路徑就會顯示在 **[位置]** 方塊中。  
  
## <a name="registering-the-code-snippet"></a>註冊程式碼片段  
 在建立程式碼片段檔案之後，請使用程式碼片段管理員，向 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]註冊程式碼片段。 您可以加入包含多個程式碼片段的資料夾，或是將個別程式碼片段匯入到 **[My Code 程式碼片段]** 資料夾。  
  
## <a name="procedures"></a>程序  
  
#### <a name="adding-a-snippet-folder"></a>加入程式碼片段資料夾  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
2.  選取 **[工具]** 功能表，然後按一下 **[程式碼片段管理員]**。  
  
3.  按一下 **[加入]** 按鈕。  
  
4.  導覽至包含程式碼片段的資料夾，然後按一下 **[選取資料夾]** 按鈕。  
  
#### <a name="importing-a-snippet"></a>匯入程式碼片段  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
2.  選取 **[工具]** 功能表，然後按一下 **[程式碼片段管理員]**。  
  
3.  按一下 **[匯入]** 按鈕。  
  
4.  導覽至包含程式碼片段的資料夾，然後按一下 .snippet 檔案，再按一下 **[開啟]** 按鈕。  
  
## <a name="examples"></a>範例  
 下列範例會建立`TRY-CATCH`範圍陳述式程式碼片段並將它匯入[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
1.  將下列程式碼貼到 [記事本]，然後將檔案儲存為 TryCatch.snippet 名稱。  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">  
    <_locDefinition xmlns="urn:locstudio">  
        <_locDefault _loc="locNone" />  
        <_locTag _loc="locData">Title</_locTag>  
        <_locTag _loc="locData">Description</_locTag>  
        <_locTag _loc="locData">Author</_locTag>  
        <_locTag _loc="locData">ToolTip</_locTag>  
       <_locTag _loc="locData">Default</_locTag>  
    </_locDefinition>  
    <CodeSnippet Format="1.0.0">  
    <Header>  
    <Title>TryCatch</Title>  
                            <Shortcut></Shortcut>  
    <Description>Example Snippet for Try-Catch.</Description>  
    <Author>SQL Server Books Online Example</Author>  
    <SnippetTypes>  
                                    <SnippetType>SurroundsWith</SnippetType>  
    </SnippetTypes>  
    </Header>  
    <Snippet>  
    <Declarations>  
                                    <Literal>  
                                    <ID>CatchCode</ID>  
                                    <ToolTip>Code to handle the caught error</ToolTip>  
                                    <Default>CatchCode</Default>  
                                    </Literal>  
    </Declarations>  
    <Code Language="SQL"><![CDATA[  
    BEGIN TRY  
  
    $selected$ $end$  
  
    END TRY  
    BEGIN CATCH  
  
    $CatchCode$  
  
    END CATCH;  
    ]]>  
    </Code>  
    </Snippet>  
    </CodeSnippet>  
    </CodeSnippets>  
    ```  
  
2.  開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
3.  選取 **[工具]** 功能表，然後按一下 **[程式碼片段管理員]**。  
  
4.  按一下 **[匯入]** 按鈕。  
  
5.  導覽至包含 TryCatch.snippet 的資料夾，然後按一下 TryCatch.snippet 檔案，再按一下 **[開啟]** 按鈕。 **[My Code 程式碼片段]** 資料夾中應該不會有 TryCatch 程式碼片段。  
  
## <a name="see-also"></a>另請參閱  
 [插入範圍陳述式 Transact-SQL 程式碼片段](insert-surround-with-transact-sql-snippets.md)  
  
  
