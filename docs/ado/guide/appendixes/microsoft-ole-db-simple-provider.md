---
description: Microsoft OLE DB 簡單提供者總覽
title: Microsoft OLE DB 簡單提供者 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- simple provider [ADO]
- providers [ADO], OLE DB simple provider
- OLE DB simple provider [ADO]
ms.assetid: 1e7dc6f0-482c-4103-8187-f890865e40fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 9ed83809ec1bf3fd4ba55552f4ecac1d55cfb8d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454020"
---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Microsoft OLE DB 簡單提供者總覽
Microsoft OLE DB Simple Provider (OSP) 可讓 ADO 存取任何已使用 [OLE DB Simple provider (OSP) 工具](https://msdn.microsoft.com/6e7b7931-9e4a-4151-ae51-672abd3f84a6)組撰寫提供者的資料。 簡單提供者旨在存取只需要基本 OLE DB 支援的資料來源，例如記憶體中的陣列或 XML 檔。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到 OLE DB Simple Provider DLL，請將[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性的*Provider*引數設定為：

```vb
MSDAOSP
```

 您也可以使用 [Provider](../../../ado/reference/ado-api/provider-property-ado.md) 屬性來設定或讀取這個值。

 您可以使用已註冊的提供者名稱（由提供者寫入器所決定），連接到已註冊為完整 OLE DB 提供者的簡單提供者。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串為：

```vb
"Provider=MSDAOSP;Data Source=serverName"
```

 此字串包含下列關鍵字：

|關鍵字|描述|
|-------------|-----------------|
|**提供者**|指定 SQL Server 的 OLE DB 提供者。|
|**資料來源**|指定伺服器的名稱。|

## <a name="xml-document-example"></a>XML 檔範例
 OLE DB 的簡單提供者 (在 MDAC 2.7 或更新版本中的 OSP) ，以及 (Windows DAC) 的 Windows 資料存取元件都已增強，可支援透過任意 XML 檔案開啟階層式 ADO **記錄集** 。 這些 XML 檔案可能包含 ADO XML 持續性架構，但不是必要的。 這是藉由將 OSP 連接到 **MSXML2.DLL**來實現;因此 **MSXML2.DLL** 或更新版本是必要的。

 下列範例中使用的 **portfolio.xml** 檔案包含下列樹狀結構：

```console
Portfolio
   Stock
      Shares
      Symbol
      Price
      Info
         Company Name
         WebSite
```

 XML DSO 使用內建的啟發學習法，將 XML 樹狀結構中的節點轉換成階層式 **記錄集中**的章節。

 使用這些內建啟發學習法，會將 XML 樹狀結構轉換成下列格式的兩層式階層式 **記錄集** ：

```console
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 請注意，「組合」和「資訊」標記不會以階層式 **記錄集**表示。 如需 XML DSO 如何將 XML 樹狀結構轉換成階層式 **記錄集**的說明，請參閱下列規則。 下一節將討論 $Text 資料行。

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>將 XML 元素和屬性指派給資料行和資料列的規則
 XML DSO 遵循將專案和屬性指派給資料系結應用程式中之資料行和資料列的程式。 XML 會模型化為樹狀結構，其中包含一個包含整個階層的標記。 例如，書籍的 XML 描述可以包含章節標記、圖標籤和區段標記。 最高層級會是書籍標記，其中包含子項目章節、圖和區段。 當 XML DSO 將 XML 元素對應到資料列和資料行時，會轉換子項目，而不是最上層專案。

 XML DSO 會使用這個程式來轉換子項目：

-   每個子項目和屬性都會對應到階層中某些 **記錄集** 內的資料行。

-   資料行的名稱與子項目或屬性的名稱相同，除非父項目具有相同名稱的屬性和子項目，在此情況下，子專案的資料行名稱前面會加上 "！"。

-   每個資料行都是簡單的資料行，其中包含*純*量值 (通常是字串) 或包含子**記錄**集的**記錄集**資料行。

-   對應至屬性的資料行一律很簡單。

-   如果子項目有自己的子項目或屬性 (或兩者都) ，或子項目的父系有一個以上的子項目實例做為子系，則對應至子項目的資料行會是 **記錄集** 資料行。 否則，資料行很簡單。

-   當子項目有多個實例 (在不同的父系) 下，如果*任何*實例都代表**記錄集**資料行，其資料行就會是**記錄集**資料行;只有當*所有實例都*代表一個簡單的資料行時，其資料行才會很簡單。

-   所有 **記錄集** 都有一個名為 $Text 的額外資料行。

 建立 **記錄集** 所需的程式碼如下所示：

```vb
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "https://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  您可以使用四種不同的命名慣例來指定資料檔案的路徑。

```vb
'HTTP://
adoRS.Open "https://WebServer/VRoot/portfolio.xml", adoConn
'FILE://
adoRS.Open "file:/// C:\\Directory\\portfolio.xml", adoConn
'UNC Path
adoRS.Open "\\ComputerName\ShareName\portfolio.xml", adoConn
'Full DOS Path
adoRS.Open "C:\Directory\portfolio.xml", adoConn
```

 一旦開啟 **記錄集** ，就可以使用一般的 ADO **記錄集** 流覽命令。

 OSP 產生的**記錄集**有一些限制：

-   不支援 (**adUseClient**) 的用戶端資料指標。

-   無法使用**記錄集**來保存透過任意 XML 建立的階層式**記錄**集。請儲存。

-   使用 OSP 建立的**記錄集**是唯讀的。

-   XMLDSO 會將額外的資料行 ($Text) 加入至階層中的每個 **記錄集** 。

 如需 OLE DB 簡單提供者的詳細資訊，請參閱 [建立簡單的提供者](https://msdn.microsoft.com/b31a6cba-58ae-4ee8-9039-700973d354d6)。

## <a name="code-example"></a>程式碼範例
 下列 Visual Basic 程式碼示範如何開啟任意的 XML 檔案、建立階層式 **記錄集**，以及以遞迴方式將每個 **記錄集** 的每一筆記錄寫入至 [偵錯工具] 視窗。

 以下是包含股票報價的簡單 XML 檔案。 下列程式碼會使用此檔案來建立兩層階層式 **記錄集**。

```xml
<portfolio>
   <stock>
      <shares>100</shares>
      <symbol>MSFT</symbol>
      <price>$70.00</price>
      <info>
         <companyname>Microsoft Corporation</companyname>
         <website>https://www.microsoft.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>AAPL</symbol>
      <price>$107.00</price>
      <info>
         <companyname>Apple Computer, Inc.</companyname>
         <website>https://www.apple.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>DELL</symbol>
      <price>$50.00</price>
      <info>
         <companyname>Dell Corporation</companyname>
         <website>https://www.dell.com</website>
      </info>
    </stock>
    <stock>
       <shares>100</shares>
       <symbol>INTC</symbol>
       <price>$115.00</price>
       <info>
          <companyname>Intel Corporation</companyname>
          <website>https://www.intel.com</website>
       </info>
   </stock>
</portfolio>
```

 以下是兩個 Visual Basic sub 程式。 第一個會建立**記錄集**，並將它傳遞至*WalkHier* sub 程式，此程式會以遞迴方式向下切入階層，將每個記錄**集**內每筆記錄中的每個**欄位**都寫入至 [偵錯工具]

```vb
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
    adoRS.Open "https://bwillett3/Kowalski/portfolio.xml", adoConn

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
