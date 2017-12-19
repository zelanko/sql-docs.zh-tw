---
title: "使用資料錄集目的地 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Recordset destination
ms.assetid: a7b143dc-8008-404f-83b0-b45ffbca6029
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f7cf8f2ed8875856da5756288c8e3fb707f1a397
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="use-a-recordset-destination"></a>使用資料錄集目的地
  資料錄集目的地不會將資料儲存到外部資料來源， 而是將資料儲存到資料類型為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Object **之** 封裝變數內儲存的資料錄集記憶體中。 當資料錄集目的地儲存資料之後，您通常要使用具有 Foreach ADO 列舉值的 Foreach 迴圈容器來一次處理資料錄集的一個資料列。 Foreach ADO 列舉值會將目前資料列的每一資料行值儲存到個別封裝變數之中。 接著，您在 Foreach 迴圈容器中設定的工作會讀取這些變數中的值，然後對它們執行一些動作。  
  
 您可以在多種不同情況下使用資料錄集目的地。 以下是一些範例：  
  
-   您可以使用傳送郵件工作和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 運算式語言，為資料錄集的每個資料列傳送自訂的電子郵件訊息。  
  
-   您可以將指令碼元件設定成資料流程工作中的來源，然後使用該指令碼元件將資料行值讀入資料流程的資料行中。 然後，您可以使用轉換和目的地來轉換和儲存資料列。 在這個範例中，資料流程工作會為每一個資料列執行一次。  
  
 下列章節會先說明使用資料錄集目的地的一般程序，然後提供一個如何使用目的地的明確範例。  
  
## <a name="general-steps-to-using-a-recordset-destination"></a>使用資料錄集目的地的一般步驟  
 下列程序摘要列出如何將資料儲存到資料錄集目的地，然後使用 Foreach 迴圈容器處理每一個資料列的步驟。  
  
#### <a name="to-save-data-to-a-recordset-destination-and-process-each-row-by-using-the-foreach-loop-container"></a>將資料儲存到資料錄集目的地並使用 Foreach 迴圈容器處理每一個資料列  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，建立或開啟 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  建立一個變數，在其中加入由資料錄集目的地儲存到記憶體中的資料錄集，然後將變數類型設為 **Object**。  
  
3.  建立其他適當類型的變數，在其中加入您要使用之資料錄集的每一資料行值。  
  
4.  根據您計劃用於資料流程中的資料來源，新增並設定需要的連接管理員。  
  
5.  將資料流程工作加入封裝中，然後在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師的 [資料流程] 索引標籤上，設定用於載入和轉換資料的來源與轉換。  
  
6.  將資料錄集目的地加入資料流程中，然後將它連接到轉換。 為資料錄集目的地的 **VariableName** 屬性，輸入您為了保存資料錄集所建立的變數名稱。  
  
7.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師的 [控制流程] 索引標籤上，加入 Foreach 迴圈容器並將此容器連接在資料流程工作之後。 然後，開啟 Foreach 迴圈編輯器並依照下列設定來設定容器：  
  
    1.  在 [集合] 頁面上，選取 [Foreach ADO 列舉值]。 然後，為 [ADO 物件來源變數] 選取包含資料錄集的變數。  
  
    2.  在 [變數對應] 頁面上，將您要使用的每一個資料行以零為基底之索引對應到適當的變數。  
  
         在迴圈的每個反覆運算中，列舉值會使用目前資料列中的資料行值來擴展這些變數。  
  
8.  在 Foreach 迴圈容器中加入並設定工作，藉由讀取變數中的值，一次處理資料錄集的一個資料列。  
  
## <a name="example-of-using-the-recordset-destination"></a>使用資料錄集目的地的範例  
 在下列範例中，資料流程工作會將 Sales.SalesPerson 資料表中有關 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 員工的資料載入資料錄集目的地中。 然後，Foreach 迴圈容器會一次讀取一個資料列，接著呼叫傳送郵件工作。 傳送郵件工作會使用運算式，將每位銷售人員的獎金金額以自訂的電子郵件訊息傳送給每位銷售人員。  
  
#### <a name="to-create-the-project-and-configure-the-variables"></a>建立專案和設定變數  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中，建立新的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [SSIS] 功能表上，選取 [變數]。  
  
3.  在 [變數] 視窗中建立變數，用以保存資料錄集和目前資料列的資料行值：  
  
    1.  建立名稱為 **BonusRecordset** 的變數，並將其類型設為 **Object**。  
  
         **BonusRecordset** 變數會保存資料錄集。  
  
    2.  建立名稱為 **EmailAddress**的變數，並將其類型設為 **String**。  
  
         **EmailAddress** 變數會保存銷售人員的電子郵件地址。  
  
    3.  建立名稱為 **FirstName**的變數，然後將其類型設為 **String**。  
  
         **FirstName** 變數會保存銷售人員的名字。  
  
    4.  建立名稱為 **Bonus**的變數，然後將其類型設為 **Double**。  
  
         **Bonus** 變數會保存銷售人員的獎金金額。  
  
#### <a name="to-configure-the-connection-managers"></a>設定連接管理員  
  
1.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師的「連線管理員」區域中，加入並設定連接到 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 範例資料庫的新 OLE DB 連線管理員。  
  
     資料流程工作中的 OLE DB 來源，將會使用此連接管理員進行資料擷取。  
  
2.  在「連接管理員」區域中，加入並設定連接到可用 SMTP 伺服器的新 SMTP 連接管理員。  
  
     Foreach 迴圈容器中的傳送郵件工作，將會使用此連接管理員傳送電子郵件。  
  
#### <a name="to-configure-the-data-flow-and-the-recordset-destination"></a>設定資料流程和資料錄集目的地  
  
1.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師的 [控制流程] 索引標籤上，將資料流程工作加入設計介面。  
  
2.  在 [資料流程] 索引標籤上，將 OLE DB 來源加入至資料流程工作，然後開啟 OLE DB 來源編輯器。  
  
3.  在編輯器的 [連線管理員] 頁面上，依照下列設定來設定來源：  
  
    1.  針對 [OLE DB 連線管理員]，選取您先前建立的 OLE DB 連線管理員。  
  
    2.  針對 [資料存取模式]，選取 [SQL 命令]。  
  
    3.  針對 [SQL 命令文字]，輸入下列查詢：  
  
        ```sql 
        SELECT     Person.Contact.EmailAddress, Person.Contact.FirstName, CONVERT(float, Sales.SalesPerson.Bonus) AS Bonus  
        FROM         Sales.SalesPerson INNER JOIN  
                              Person.Contact ON Sales.SalesPerson.SalesPersonID = Person.Contact.ContactID  
        ```  
  
        > [!NOTE]  
        >  您必須將 Bonus 資料行中的 **currency** 值轉換為 **float**，然後才能將此值載入 **Double** 類型的封裝變數中。  
  
4.  在 [資料流程] 索引標籤上，加入資料錄集目的地，然後將目的地連接到 OLE DB 來源之後。  
  
5.  開啟資料錄集目的地編輯器，並依照下列設定來設定目的地：  
  
    1.  在 [元件屬性] 索引標籤上，為 [VariableName] 屬性選取 [User::BonusRecordset]。  
  
    2.  在 [輸入資料行] 索引標籤上，選取可用的全部三個資料行。  
  
#### <a name="to-configure-the-foreach-loop-container-and-run-the-package"></a>設定 Foreach 迴圈容器並執行封裝  
  
1.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師的 [控制流程] 索引標籤上，加入 Foreach 迴圈容器，並將此容器連接在資料流程工作之後。  
  
2.  開啟 Foreach 迴圈編輯器，依照下列設定來設定容器：  
  
    1.  在 [集合] 頁面上，為 [列舉值] 選取 [Foreach ADO 列舉值]，然後為 [ADO 物件來源變數] 選取 [User::BonusRecordset]。  
  
    2.  在 [變數對應] 頁面上，將 [User::EmailAddress] 對應到索引 0、將 [User::FirstName] 對應到索引 1，然後將 [User::Bonus] 對應到索引 2。  
  
3.  在 [控制流程] 索引標籤上的 Foreach 迴圈容器中，加入傳送郵件工作。  
  
4.  開啟傳送郵件工作編輯器，然後在 [郵件] 頁面上，依照下列設定來設定工作：  
  
    1.  針對 [SmtpConnection]，選取先前設定的 SMTP 連線管理員。  
  
    2.  針對 [From]，輸入適當的電子郵件地址。  
  
         如果使用您自己的電子郵件地址，可以確認封裝是否成功執行。 針對由傳送郵件工作傳送到 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 虛構銷售人員的郵件，您將會收到無法傳遞的收件者訊息。  
  
    3.  針對 [To]，輸入預設的電子郵件地址。  
  
         雖然不會使用這個值，但是這個值會在執行階段由各銷售人員的電子郵件地址所取代。  
  
    4.  針對 [Subject]，輸入「您的年度獎金」。  
  
    5.  針對 [MessageSourceType]，選取 [直接輸入]。  
  
5.  在傳送郵件工作編輯器的 [運算式] 頁面上，按一下省略符號按鈕 (**...**) 以開啟屬性運算式編輯器。  
  
6.  在屬性運算式編輯器中，輸入下列資訊：  
  
    1.  針對 [ToLine]，加入下列運算式：  
  
        ```  
        @[User::EmailAddress]  
        ```  
  
    2.  針對 [MessageSource] 屬性，加入下列運算式：  
  
        ```  
        "Dear " +  @[User::FirstName] + ": The amount of your bonus for this year is $" +  (DT_WSTR, 12) @[User::Bonus] + ". Thank you!"  
        ```  
  
7.  執行封裝。  
  
     如果您指定了有效的 SMTP 伺服器且提供您自己的電子郵件地址，針對由傳送郵件工作傳送到 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]虛構銷售人員的郵件，您將會收到無法傳遞的收件者訊息。  
  
  
