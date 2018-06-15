---
title: Microsoft OLE DB 簡單提供者 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- simple provider [ADO]
- providers [ADO], OLE DB simple provider
- OLE DB simple provider [ADO]
ms.assetid: 1e7dc6f0-482c-4103-8187-f890865e40fc
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d3abb4d2d34220800a1d8c71b6227cc8de0fd88
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271517"
---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Microsoft OLE DB 簡單提供者概觀
Microsoft OLE DB 簡單提供者 (OSP) 可讓 ADO 存取任何資料的提供者已寫入使用[OLE DB 簡單提供者 (OSP) 工具組](http://msdn.microsoft.com/en-us/6e7b7931-9e4a-4151-ae51-672abd3f84a6)。 簡單的提供者被用來存取資料來源需要唯一基本的 OLE DB 支援，例如記憶體中陣列或 XML 文件。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到 OLE DB 簡單提供者 DLL，請設定*提供者*引數[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性：

```
MSDAOSP
```

 這個值也可以設定或讀取使用[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性。

 您可以連接到已註冊為完整的 OLE DB 提供者使用的已註冊的提供者名稱，取決於提供者撰寫人員的簡單提供者。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串是：

```
"Provider=MSDAOSP;Data Source=serverName"
```

 字串，包含這些關鍵字：

|關鍵字|描述|
|-------------|-----------------|
|**提供者**|指定 SQL Server 的 OLE DB 提供者。|
|**資料來源**|指定伺服器的名稱。|

## <a name="xml-document-example"></a>XML 文件範例
 OLE DB 簡單提供者 (OSP) 在 MDAC 2.7 版或更新版本以及 Windows Data Access Components (Windows DAC) 已增強為支援開啟階層式 ADO**資料錄集**比任意 XML 檔案。 這些 XML 檔案可能包含 ADO XML 持續性結構描述，但並非必要。 這已藉由連接到 OSP 實作**MSXML2.DLL**; 因此**MSXML2.DLL**或更新版本。

 **Portfolio.xml**用在下列範例中的檔案包含下列樹狀結構：

```
Portfolio
   Stock
      Shares
      Symbol
      Price
      Info
         Company Name
         WebSite
```

 XML DSO 會使用內建的啟發式來轉換 XML 樹狀結構中的節點在階層式章節**資料錄集**。

 使用這些內建的啟發學習法，XML 樹狀結構會轉換成兩個層級階層式**資料錄集**的格式如下：

```
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 請注意階層中並無代表 Portfolio 和資訊標記**資料錄集**。 如需說明 XML DSO 如何將 XML 樹狀結構轉換為階層式**資料錄集**，請參閱下列規則。 在下一節討論 $Text 資料行。

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>指定 XML 元素和屬性資料行和資料列的規則
 XML DSO 會遵循的程序，指派項目和屬性，將資料行和資料繫結應用程式中的資料列。 XML 是模型化為具有一個標籤，其中包含整個階層的樹狀目錄。 例如，活頁簿的 XML 描述可能包含章標記、 圖標籤和區段標記。 最高的層級會是包含子元素章節，圖中和區段的活頁簿標記。 當 XML DSO 會對應至資料列和資料行的 XML 項目時，子項目，而不是最上層項目，會轉換。

 XML DSO 會使用這個程序的轉換子元素：

-   每一個子元素和屬性對應到資料行，在某些**資料錄集**階層中。

-   資料行的名稱會做為子元素或屬性的名稱相同，除非父項目可具有的屬性和子元素具有相同的名稱，在此情況下"！"子元素的資料行名稱前面加上。

-   每個資料行是*簡單*資料行包含純量值 （通常是字串） 或**資料錄集**含有子系的資料行**資料錄集**。

-   資料行對應到屬性一定是簡單的。

-   資料行對應到子元素是**資料錄集**如果子元素都具有自己的子元素或屬性 （或兩者），或是子元素的父代具有子元素做為子系的多個執行個體的資料行。 否則，資料行是簡單的。

-   當有多個執行個體的子元素 （在不同的父代） 時，其資料行是**資料錄集**資料行如果*任何*的執行個體代表**資料錄集**資料行，其資料行是簡單才*所有*執行個體代表簡單的資料行。

-   所有**資料錄集**具有名為 $Text 額外的資料行。

 程式碼所需建構**資料錄集**如下所示：

```
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "http://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  使用四個不同的命名慣例，可以指定資料檔案的路徑。

```
'HTTP://
adoRS.Open "http://WebServer/VRoot/portfolio.xml", adoConn
'FILE://
adoRS.Open "file:/// C:\\Directory\\portfolio.xml", adoConn
'UNC Path
adoRS.Open "\\ComputerName\ShareName\portfolio.xml", adoConn
'Full DOS Path
adoRS.Open "C:\Directory\portfolio.xml", adoConn
```

 只要**資料錄集**已開啟，一般 ADO**資料錄集**巡覽命令可用。

 **資料錄集**產生 OSP 有一些限制：

-   用戶端資料指標 (**adUseClient**) 不支援。

-   階層式**資料錄集**建立任意 XML 無法保存使用**Recordset.Save**。

-   **資料錄集**以 OSP 建立處於唯讀狀態。

-   XMLDSO 將額外的資料行的資料 ($Text) 加入至每個**資料錄集**階層中。

 如需有關 OLE DB 簡單提供者的詳細資訊，請參閱[建置簡單的提供者](http://msdn.microsoft.com/en-us/b31a6cba-58ae-4ee8-9039-700973d354d6)。

## <a name="code-example"></a>程式碼範例
 下列 Visual Basic 程式碼示範如何開啟任意 XML 檔案，建構一個階層式**資料錄集**，並以遞迴方式撰寫每一筆記錄，每個**資料錄集**的偵錯視窗。

 以下是簡單的 XML 檔案，其中包含股票報價。 下列程式碼會使用此檔案，以建構兩個層級階層式**資料錄集**。

```
<portfolio>
   <stock>
      <shares>100</shares>
      <symbol>MSFT</symbol>
      <price>$70.00</price>
      <info>
         <companyname>Microsoft Corporation</companyname>
         <website>http://www.microsoft.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>AAPL</symbol>
      <price>$107.00</price>
      <info>
         <companyname>Apple Computer, Inc.</companyname>
         <website>http://www.apple.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>DELL</symbol>
      <price>$50.00</price>
      <info>
         <companyname>Dell Corporation</companyname>
         <website>http://www.dell.com</website>
      </info>
    </stock>
    <stock>
       <shares>100</shares>
       <symbol>INTC</symbol>
       <price>$115.00</price>
       <info>
          <companyname>Intel Corporation</companyname>
          <website>http://www.intel.com</website>
       </info>
   </stock>
</portfolio>
```

 以下是兩個 Visual Basic sub 程序。 第一個建立**資料錄集**並將其傳遞給*WalkHier* sub 程序中，遞迴階層中向下，撰寫每個所引導**欄位**中每個中的每一筆記錄**資料錄集**的偵錯視窗。

```
Private Sub BrowseHierRecordset()
' Add ADO 2.7 or later to Project/References
' No need to add MSXML2, ADO just passes the ProgID through to the OSP.

    Dim adoConn As ADODB.Connection
    Dim adoRS As ADODB.Recordset
    Dim adoChildRS As ADODB.Recordset

    Set adoConn = New ADODB.Connection
    Set adoRS = New ADODB.Recordset
    Set adoChildRS = ADODB.Recordset

    adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
    adoRS.Open "http://bwillett3/Kowalski/portfolio.xml", adoConn

    Dim iLevel As Integer
    iLevel = 0
    WalkHier iLevel, adoRS

End Sub

Sub WalkHier(ByVal iLevel As Integer, ByVal adoRS As ADODB.Recordset)
    iLevel = iLevel + 1
    PriorLevel = iLevel
    While Not adoRS.EOF
        For ndx = 0 To adoRS.Fields.Count - 1
            If adoRS.Fields(ndx).Name <> "$Text" Then
                If adoRS.Fields(ndx).Type = adChapter Then
                    Set adoChildRS = adoRS.Fields(ndx).Value
                    WalkHier iLevel, adoChildRS
                Else
                    Debug.Print iLevel & ": adoRS.Fields(" & ndx & _
                       ") = " & adoRS.Fields(ndx).Name & " = " & _
                       adoRS.Fields(ndx).Value
                End If
            End If
        Next ndx
        adoRS.MoveNext
    Wend
    iLevel = PriorLevel
End Sub
```
