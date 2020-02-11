---
title: Visual C++ ADO 程式設計 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO]
ms.assetid: 11233b96-e05c-4221-9aed-5f20944b0f1c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1890d554367b2a21bcd46a6d2ebddf00013957e6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926427"
---
# <a name="visual-c-ado-programming"></a>Visual C++ ADO 程式設計
ADO API 參考會使用類似于 Microsoft Visual Basic 的語法來描述 ADO 應用程式開發介面（API）的功能。 雖然目標物件是所有使用者，但 ADO 程式設計人員會採用各種語言，例如 Visual Basic、Visual C++ （不論是否使用 **#import**指示詞）和 Visual j + + （使用 ADO/WFC 類別套件）。  

> [!NOTE]
> Microsoft 已于2004結束對 Visual j + + 的支援。

 為了因應這項多樣性， [Visual C++ 語法索引的 ADO](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)提供了 Visual C++ 特定語言的語法，並連結至 API 參考中的功能、參數、例外行為等等的一般描述。  
  
 ADO 是使用 COM （元件物件模型）介面來執行。 不過，程式設計人員可以更輕鬆地使用特定程式語言中的 COM，而不是其他語言。 例如，幾乎所有使用 COM 的細節都是針對 Visual Basic 程式設計人員隱含處理，而 Visual C++ 程式設計人員必須親自參與這些細節。  
  
 下列各節摘要說明使用 ADO 和 **#import**指示詞之 c 和 c + + 程式設計人員的詳細資料。 它著重于 COM （**Variant**、 **BSTR**和**SafeArray**）專屬的資料類型，以及錯誤處理（_com_error）。  
  
## <a name="using-the-import-compiler-directive"></a>使用 #import 編譯器指示詞  
 **#Import** Visual C++ 編譯器指示詞可簡化使用 ADO 方法和屬性的作業。 指示詞會採用包含類型程式庫的檔案名，例如 ADO （Msado15.dll），並產生包含 typedef 宣告的標頭檔、介面的智慧型指標，以及列舉的常數。 在類別中，每個介面都會封裝或包裝。  
  
 針對類別中的每個作業（也就是方法或屬性呼叫），有一個宣告可直接呼叫作業（也就是作業的「原始」形式），以及一個宣告來呼叫原始作業，並在作業無法執行 succ 時擲回 COM 錯誤essfully. 如果作業是屬性，通常會有一個編譯器指示詞，它會針對具有類似 Visual Basic 語法的運算建立替代語法。  
  
 抓取屬性值的作業具有格式的名稱，也就是**Get**_屬性_。 設定屬性值的作業具有格式、 **Put**_屬性_的名稱。 使用 ADO 物件的指標來設定屬性值的作業，其格式為**PutRef**_屬性_的名稱。  
  
 您可以使用下列形式的呼叫來取得或設定屬性：  
  
```cpp
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```
  
## <a name="using-property-directives"></a>使用 Property 指示詞  
 **__Declspec （屬性 ...）** 編譯器指示詞是 Microsoft 專有的 C 語言延伸模組，它會宣告用來做為屬性的函式，以具有替代語法。 因此，您可以使用類似于 Visual Basic 的方式來設定或取得屬性的值。 例如，您可以透過這種方式來設定和取得屬性：  
  
```cpp
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```
  
 請注意，您不需要撰寫程式碼：  
  
```cpp
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```
  
 編譯器會根據所宣告的替代語法，以及是否要讀取或寫入屬性，來產生適當的**Get**_-_、 **Put**或**PutRef**_屬性_呼叫。  
  
 **__Declspec （屬性 ...）** 編譯器指示詞只能宣告**get**、 **put**或**get**和**put**函數的替代語法。 唯讀作業只有**get**宣告;僅限寫入的作業只有**put**宣告;同時為讀取和寫入的作業都有**get**和**put**宣告。  
  
 這個指示詞只能有兩個宣告;不過，每個屬性可能會有三個屬性函數： **Get**_property_、 **Put**_屬性_和**PutRef**_屬性_。 在這種情況下，只有兩種形式的屬性會有替代語法。  
  
 例如，**命令**物件**ActiveConnection**屬性是以**Get**_ActiveConnection_和**PutRef**_ActiveConnection_的替代語法來宣告。 **PutRef**語法是不錯的選擇，因為在實務上，您通常會想要將開啟的**連接**物件（也就是**連接**物件指標）放在這個屬性中。 另一方面，**記錄集**物件有**Get**-、 **Put**和**PutRef**_ActiveConnection_作業，但沒有替代語法。  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>集合、GetItem 方法和 Item 屬性  

 ADO 定義數個集合，包括**欄位**、**參數**、**屬性**和**錯誤**。 在 Visual C++ 中， **GetItem （_index_）** 方法會傳回集合的成員。 *Index*是**Variant**，其值為集合中成員的數值索引，或包含成員名稱的字串。  
  
 **__Declspec （屬性 ...）** 編譯器指示詞會將**Item**屬性宣告為每個集合基本**GetItem （）** 方法的替代語法。 替代語法會使用方括弧，看起來類似陣列參考。 一般而言，這兩種表單看起來像下面這樣：  
  
```cpp
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```
  
 例如，將值指派給名為**_rs_** 之**記錄集**物件的欄位，衍生自**pubs**資料庫的**作者**資料表。 使用**Item （）** 屬性存取**記錄集**物件**欄位**集合的第三個**欄位**（集合會從零編制索引，假設第三個欄位命名**_為\_au fname_**）。 然後在**Field**物件上呼叫**Value （）** 方法來指派字串值。  
  
 這可以使用下列四種方式以 Visual Basic 表示（最後兩個表單對 Visual Basic 而言是唯一的，而其他語言則沒有對等專案）：  
  
```cpp
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```
  
 在上述的前兩個表單 Visual C++ 中，對等項是：  
  
```cpp
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```
  
 -或-（也會顯示**Value**屬性的替代語法）  
  
```cpp
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```
  
 如需逐一查看集合的範例，請參閱「ADO 參考」的「ADO 集合」一節。  
  
## <a name="com-specific-data-types"></a>COM 特有的資料類型  
 一般而言，您在 ADO API 參考中找到的任何 Visual Basic 資料類型都有 Visual C++ 對等的。 其中包括標準資料類型（例如不**帶正負**號的 char 用於 Visual Basic 的**位元組**）、**整數**的**** **short** **，以及 long** 。 查看語法 Indexesto，以確切查看給定方法或屬性的運算元所需的內容。  
  
 此規則的例外狀況是 COM 特有的資料類型： **Variant**、 **BSTR**和**SafeArray**。  
  
### <a name="variant"></a>變數  
 **Variant**是包含值成員和資料型別成員的結構化資料型別。 **Variant**可以包含各式各樣的其他資料類型，包括另一個 VARIANT、BSTR、Boolean、IDispatch 或 IUnknown 指標、貨幣、日期等等。 COM 也提供方法，讓您輕鬆地將一種資料類型轉換成另一種。  
  
 **_Variant_t**類別會封裝和管理**variant**資料類型。  
  
 當 ADO API 參考指出方法或屬性運算元接受值時，通常表示會在 **_variant_t**中傳遞值。  
  
 當 ADO API 參考主題中的**Parameters**區段指出運算元是**Variant**時，此規則會明確成立。 其中一個例外狀況是當檔明確指出運算元採用標準資料類型（例如**Long**或**Byte**）或列舉時。 另一個例外狀況是運算元採用**字串**時。  
  
### <a name="bstr"></a>BSTR  
 **BSTR** （**B**asic **STR**）是包含字元字串和字串長度的結構化資料類型。 COM 提供配置、操作和釋放**BSTR**的方法。  
  
 **_Bstr_t**類別會封裝和管理**bstr**資料類型。  
  
 當 ADO API 參考指出方法或屬性接受**字串**值時，表示值的格式為 **_bstr_t**。  
  
### <a name="casting-_variant_t-and-_bstr_t-classes"></a>轉換 _variant_t 和 _bstr_t 類別  
 通常不需要在作業的引數中明確地將 **_variant_t**或 **_bstr_t**編碼。 如果 **_variant_t**或 **_bstr_t**類別的函式與引數的資料類型相符，則編譯器會產生適當的 **_variant_t**或 **_bstr_t**。  
  
 不過，如果引數不明確（也就是引數的資料類型）符合一個以上的函式，您就必須使用適當的資料類型來轉換引數，以叫用正確的處理常式。  
  
 例如，**記錄集：： Open**方法的宣告為：  
  
```cpp
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```
  
 引數會取得 **_variant_t**的參考，您可以將其編碼為連接字串或開啟連線物件的指標。 **** `ActiveConnection`  
  
 如果您**** 傳遞 "`DSN=pubs;uid=MyUserName;pwd=MyPassword;`" 之類的字串或指標（例如 "`(IDispatch *) pConn`"），則會隱含地建立正確的 _variant_t。  
  
> [!NOTE]
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在連接字串中指定**Trusted_Connection = yes**或**整合式安全性 = SSPI** ，而不是使用者識別碼和密碼資訊。  
  
 或者，您可以明確地將包含指標的 **_variant_t**程式碼`_variant_t((IDispatch *) pConn, true)`，例如 ""。 轉型會`(IDispatch *)`使用另一個接受 IUnknown 介面指標的函式來解析不明確的。  
  
 這是很重要的，但是很少提到，ADO 是 IDispatch 介面。 每當 ADO 物件的指標必須以**Variant**形式傳遞時，該指標必須轉換成 IDispatch 介面的指標。  
  
 最後一個案例會使用的選擇性預設值，以明確的方式，將此函式`true`的第二個布林引數編碼。 這個引數會使**Variant**函式呼叫其**AddRef**（）方法，這會在 ado 方法或屬性呼叫完成時，補償 ado 自動呼叫 **_variant_t：： Release**（）方法。  
  
### <a name="safearray"></a>SafeArray  
 **SafeArray**是結構化資料類型，其中包含其他資料類型的陣列。 **SafeArray**稱為「*安全*」，因為它包含每個陣列維度之界限的相關資訊，並限制對這些界限內陣列元素的存取。  
  
 當 ADO API 參考指出方法或屬性採用或傳回陣列時，這表示方法或屬性會接受或傳回**SafeArray**，而不是原生 C/c + + 陣列。  
  
 例如，**連接**物件**OpenSchema**方法的第二個參數需要**Variant**值陣列。 這些**變體**值必須當做**SafeArray**的元素傳遞，而且該**safearray**必須設定為另一個**Variant**的值。 另一個**變體**會當做**OpenSchema**的第二個引數來傳遞。  
  
 如需進一步的範例， **Find**方法的第一個引數是**Variant** ，其值為一維**SafeArray**;**AddNew**的每一個選擇性第一個和第二個引數都是一維**SafeArray**;而**GetRows**方法的傳回值是**Variant** ，其值為二維**SafeArray**。  
  
## <a name="missing-and-default-parameters"></a>遺漏和預設參數  
 Visual Basic 允許方法中遺漏參數。 例如，**記錄集**物件**Open**方法有五個參數，但您可以略過中繼參數，並保留尾端參數。 根據遺漏運算元的資料類型，將會取代預設的**BSTR**或**Variant** 。  
  
 在 C/c + + 中，必須指定所有運算元。 如果您想要指定其資料類型為字串的遺漏參數，請指定包含 null 字串的 **_bstr_t** 。 如果您想要指定資料類型為**Variant**的遺漏參數，請指定值為 DISP_E_PARAMNOTFOUND 的 **_variant_t**和 VT_ERROR 的類型。 或者，指定 **#import**指示詞所提供的對等 **_variant_t**常數**vtMissing**。  
  
 有三種方法是一般使用**vtMissing**的例外狀況。 這些是**連接**和**命令**物件的**執行**方法，以及**記錄集**物件的**NextRecordset**方法。 其簽章如下：  
  
```cpp
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```
  
 參數（ *RecordsAffected*和*參數*）是**Variant**的指標。 *參數*是一個輸入參數，它會指定包含單一參數的**Variant**位址，或將修改所執行之命令的參數陣列。 *RecordsAffected*是一個輸出參數，可指定**Variant**的位址，其中會傳回受方法影響的資料列數目。  
  
 在**命令**物件**Execute**方法中，將*參數*設定為`&vtMissing` （建議選項）或 null 指標（也就是**null**或零（0）），以指出未指定任何參數。 如果將*參數*設定為 null 指標，此方法會在內部替代**vtMissing**的對等，然後完成作業。  
  
 在所有方法中，將*RecordsAffected*設定為 null 指標，表示不應傳回受影響的記錄數目。 在此情況下，null 指標不會造成太多遺漏的參數，因為這表示方法應該捨棄受影響的記錄數目。  
  
 因此，這三種方法的程式碼如下所示：  
  
```cpp
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```
  
## <a name="error-handling"></a>錯誤處理  
 在 COM 中，大部分的作業會傳回 HRESULT 傳回碼，指出函數是否已順利完成。 **#Import**指示詞會針對每個「原始」方法或屬性產生包裝函式程式碼，並檢查傳回的 HRESULT。 如果 HRESULT 指出失敗，包裝函式程式碼會呼叫 _com_issue_errorex （）並以 HRESULT 傳回碼做為引數，以擲回 COM 錯誤。 在**try**-**catch**區塊中可以攔截 COM 錯誤物件。 （為了提高效率，請攔截 **_com_error**物件的參考）。  
  
 請記住，這些是 ADO 錯誤：這是因為 ADO 作業失敗所造成。 基礎提供者所傳回的錯誤會顯示為**連接**物件**錯誤**集合中的**錯誤**物件。  
  
 **#Import**指示詞只會為 ADO 中所宣告的方法和屬性建立錯誤處理常式。 不過，您可以藉由撰寫自己的錯誤檢查宏或內嵌函式，來利用這個相同的錯誤處理機制。 如需範例，請參閱主題、 [Visual C++ 延伸](../../../ado/guide/appendixes/visual-c-extensions-for-ado.md)模組或下列各節中的程式碼。  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Visual Basic 慣例的 Visual C++ 對應項  
 以下摘要說明 ADO 檔中的數個慣例，以 Visual Basic 撰寫程式碼，以及它們在 Visual C++ 中的對等專案。  
  
### <a name="declaring-an-ado-object"></a>宣告 ADO 物件  
 在 Visual Basic 中，ADO 物件變數（在此案例中為**記錄集**物件）會宣告如下：  
  
```vb
Dim rst As ADODB.Recordset  
```
  
 子句 "`ADODB.Recordset`" 是**記錄**檔物件的 ProgID，如登錄中所定義。 **記錄**物件的新實例會宣告如下：  
  
```vb
Dim rst As New ADODB.Recordset  
```
  
 -或-  
  
```vb
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```
  
 在 Visual C++ 中， **#import**指示詞會產生所有 ADO 物件的智慧型指標類型宣告。 例如，指向 **_Recordset**物件的變數屬於 **_RecordsetPtr**類型，且宣告如下：  
  
```cpp
_RecordsetPtr  rs;  
```
  
 指向 **_Recordset**物件之新實例的變數會宣告如下：  
  
```cpp
_RecordsetPtr  rs("ADODB.Recordset");  
```
  
 -或-  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance("ADODB.Recordset");  
```
  
 -或-  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance(__uuidof(_Recordset));  
```
  
 呼叫**CreateInstance**方法之後，您可以使用變數，如下所示：  
  
```cpp
rs->Open(...);  
```
  
 請注意，在其中一種情況`.`下，會使用 "" 運算子，如同變數是類別的實例（`rs.CreateInstance`），而在另一種情況下`->`，則會使用 "" 運算子，如同變數是介面的指標（`rs->Open`）。  
  
 有兩種方式可以使用一個變數，因為 "`->`" 運算子會多載，讓類別的實例行為就像介面的指標。 執行個體變數的私用類別成員包含 **_Recordset**介面的指標;"`->`" 運算子會傳回該指標;而傳回的指標會存取 **_Recordset**物件的成員。  
  
### <a name="coding-a-missing-parameter---string"></a>編碼遺失的參數-字串  
 當您需要在 Visual Basic 中撰寫遺漏**字串**運算元的程式碼時，您只會省略運算元。 您必須在 Visual C++ 中指定運算元。 以空字串做為值的 **_bstr_t**程式碼。  
  
```cpp
_bstr_t strMissing(L"");  
```
  
### <a name="coding-a-missing-parameter---variant"></a>撰寫遺漏參數的程式碼-Variant  
 當您需要在 Visual Basic 中撰寫遺漏的**Variant**運算元的程式碼時，您只會省略運算元。 您必須在 Visual C++ 中指定所有運算元。 使用設定為特殊值、DISP_E_PARAMNOTFOUND 和類型 VT_ERROR 的 **_variant_t** ，撰寫遺漏**Variant**參數的程式碼。 或者，指定**vtMissing**，這是 **#import**指示詞所提供的對等預先定義常數。  
  
```cpp
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```
  
 -或使用-  
  
```cpp
...vtMissing...;  
```
  
### <a name="declaring-a-variant"></a>宣告 Variant  
 在 Visual Basic 中，會使用**Dim**語句來宣告**Variant** ，如下所示：  
  
```vb
Dim VariableName As Variant  
```
  
 在 Visual C++ 中，將變數宣告為類型 **_variant_t**。 以下顯示一些示意性 **_variant_t**宣告。  
  
> [!NOTE]
>  這些宣告只是讓您大致瞭解如何在自己的程式中撰寫程式碼。 如需詳細資訊，請參閱下列範例，以及 Visual C + + 檔。  
  
```cpp
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```
  
### <a name="using-arrays-of-variants"></a>使用變體陣列  
 在 Visual Basic 中，**變數**陣列可以使用**Dim**語句來編碼，或者您可以使用**Array**函數，如下列範例程式碼所示：  
  
```vb
Public Sub ArrayOfVariants  
Dim cn As ADODB.Connection  
Dim rs As ADODB.Recordset  
Dim fld As ADODB.Field  
  
    cn.Open "DSN=pubs"  
    rs = cn.OpenSchema(adSchemaColumns, _  
        Array(Empty, Empty, "authors", Empty))  
    For Each fld in rs.Fields  
        Debug.Print "Name = "; fld.Name  
    Next fld  
    rs.Close  
    cn.Close  
End Sub  
```
  
 下列 Visual C++ 範例示範如何使用搭配 **_variant_t**使用的**SafeArray** 。  
  
#### <a name="notes"></a>注意  
 下列附注對應至程式碼範例中的批註區段。  
  
1.  同樣地，TESTHR （）內嵌函式的定義，是要利用現有的錯誤處理機制。  
  
2.  您只需要一維陣列，因此您可以使用**SafeArrayCreateVector**，而不是一般用途的**SAFEARRAYBOUND**宣告和**SafeArrayCreate**函式。 以下是該程式碼會使用**SafeArrayCreate**的樣子：  
  
    ```cpp
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```
  
3.  列舉常數**adSchemaColumns**所識別的架構與四個條件約束資料行相關聯： TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME 和 COLUMN_NAME。 因此，會建立具有四個元素的**Variant**值陣列。 然後會指定對應至第三個數據行 TABLE_NAME 的條件約束值。  
  
     傳回的**記錄集**是由數個數據行所組成，其中的子集是條件約束資料行。 每個傳回之資料列的條件約束資料行值，必須與對應的條件約束值相同。  
  
4.  熟悉**safearray**的人可能會驚訝，在結束之前不會呼叫**SafeArrayDestroy**（）。 事實上，在此情況下呼叫**SafeArrayDestroy**（）會導致執行時間例外狀況。 原因是當 **_variant_t**超出範圍時`vtCriteria` ，的析構函式會呼叫**VariantClear**（），這將會釋放**SafeArray**。 呼叫**SafeArrayDestroy**，而不手動清除 **_variant_t**，會導致析構函式嘗試清除不正確**SafeArray**指標。  
  
     如果呼叫**SafeArrayDestroy** ，程式碼看起來會像這樣：  
  
    ```cpp
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```
  
     不過，讓 **_variant_t**管理**SafeArray**更為簡單。  
  
```cpp
// Visual_CPP_ADO_Prog_1.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Note 1  
inline void TESTHR( HRESULT _hr ) {   
   if FAILED(_hr)   
      _com_issue_error(_hr);   
}  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _RecordsetPtr pRs("ADODB.Recordset");  
      _ConnectionPtr pCn("ADODB.Connection");  
      _variant_t vtTableName("authors"), vtCriteria;  
      long ix[1];  
      SAFEARRAY *pSa = NULL;  
  
      pCn->Provider = "sqloledb";  
      pCn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
      // Note 2, Note 3  
      pSa = SafeArrayCreateVector(VT_VARIANT, 1, 4);  
      if (!pSa)   
         _com_issue_error(E_OUTOFMEMORY);  
  
      // Specify TABLE_NAME in the third array element (index of 2).   
      ix[0] = 2;        
      TESTHR(SafeArrayPutElement(pSa, ix, &vtTableName));  
  
      // There is no Variant constructor for a SafeArray, so manually set the   
      // type (SafeArray of Variant) and value (pointer to a SafeArray).  
  
      vtCriteria.vt = VT_ARRAY | VT_VARIANT;  
      vtCriteria.parray = pSa;  
  
      pRs = pCn->OpenSchema(adSchemaColumns, vtCriteria, vtMissing);  
  
      long limit = pRs->GetFields()->Count;  
      for ( long x = 0 ; x < limit ; x++ )  
         printf( "%d: %s\n", x + 1, ((char*) pRs->GetFields()->Item[x]->Name) );  
      // Note 4  
      pRs->Close();  
      pCn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Error:\n");  
      printf("Code = %08lx\n", e.Error());  
      printf("Code meaning = %s\n", (char*) e.ErrorMessage());  
      printf("Source = %s\n", (char*) e.Source());  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   CoUninitialize();  
}  
```
  
### <a name="using-property-getputputref"></a>使用屬性 Get/Put/PutRef  
 在 Visual Basic 中，屬性的名稱不是由抓取、指派或指派參考所限定。  
  
```vb
Public Sub GetPutPutRef  
Dim rs As New ADODB.Recordset  
Dim cn As New ADODB.Connection  
Dim sz as Integer  
cn.Open "Provider=sqloledb;Data Source=yourserver;" & _  
         "Initial Catalog=pubs;Integrated Security=SSPI;"  
rs.PageSize = 10  
sz = rs.PageSize  
rs.ActiveConnection = cn  
rs.Open "authors",,adOpenStatic  
' ...  
rs.Close  
cn.Close  
End Sub  
```
  
 此 Visual C++ 範例示範**Get**/**Put**/**PutRef**_屬性_。  
  
#### <a name="notes"></a>注意  
 下列附注對應至程式碼範例中的批註區段。  
  
1.  這個範例使用兩種形式的遺漏字串引數：明確常數、 **strMissing**，以及編譯器將用來建立可在**Open**方法範圍記憶體在之暫時 **_bstr_t**的字串。  
  
2.  您不需要將的運算元轉換`rs->PutRefActiveConnection(cn)`為`(IDispatch *)` ，因為運算元的類型已經`(IDispatch *)`是。  
  
```cpp
// Visual_CPP_ado_prog_2.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _bstr_t strMissing(L"");  
      long oldPgSz = 0, newPgSz = 5;  
  
      // Note 1  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", strMissing, "", adConnectUnspecified);  
  
      oldPgSz = rs->GetPageSize();  
      // -or-  
      // oldPgSz = rs->PageSize;  
  
      rs->PutPageSize(newPgSz);  
      // -or-  
      // rs->PageSize = newPgSz;  
  
      // Note 2  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockReadOnly, adCmdTable);  
      printf("Original pagesize = %d, new pagesize = %d\n", oldPgSz, rs->GetPageSize());  
      rs->Close();  
      cn->Close();  
  
   }  
   catch (_com_error &e) {  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="using-getitemx-and-itemx"></a>使用 GetItem （x）和專案 [x]  
 此 Visual Basic 範例示範**Item**（）的標準和替代語法。  
  
```vb
Public Sub GetItemItem  
Dim rs As New ADODB.Recordset  
Dim name as String  
rs = rs.Open "authors", "DSN=pubs;", adOpenDynamic, _  
         adLockBatchOptimistic, adTable  
name = rs(0)  
' -or-  
name = rs.Fields.Item(0)  
rs(0) = "Test"  
rs.UpdateBatch  
' Restore name  
rs(0) = name  
rs.UpdateBatch  
rs.Close  
End Sub  
```
  
 此 Visual C++ 範例示範**專案**。  
  
> [!NOTE]
>  下列附注對應至程式碼範例中的批註區段：當使用**專案**來存取集合時，索引**2**必須轉換成**long** ，因此會叫用適當的函式。  
  
```cpp
// Visual_CPP_ado_prog_3.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
void main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _variant_t vtFirstName;  
  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", "", "", adConnectUnspecified);  
  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockOptimistic, adCmdTable);  
      rs->MoveFirst();  
  
      // Note 1. Get a field.  
      vtFirstName = rs->Fields->GetItem((long)2)->GetValue();  
      // -or-  
      vtFirstName = rs->Fields->Item[(long)2]->Value;  
  
      printf( "First name = '%s'\n", (char*)( (_bstr_t)vtFirstName) );  
  
      rs->Fields->GetItem((long)2)->Value = L"TEST";  
      rs->Update(vtMissing, vtMissing);  
  
      // Restore name  
      rs->Fields->GetItem((long)2)->PutValue(vtFirstName);  
      // -or-  
      rs->Fields->GetItem((long)2)->Value = vtFirstName;  
      rs->Update(vtMissing, vtMissing);  
      rs->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="casting-ado-object-pointers-with-idispatch-"></a>使用將 ADO 物件指標轉換成（IDispatch *）  
 下列 Visual C++ 範例示範如何使用（IDispatch *）來轉換 ADO 物件指標。  
  
#### <a name="notes"></a>注意  
 下列附注對應至程式碼範例中的批註區段。  
  
1.  以明確編碼的**Variant**指定開啟的**連接**物件。 將它轉型為\*（IDispatch），以叫用正確的函式。 此外，將第二個 **_variant_t**參數明確設定為預設值**true**，因此當**記錄集：： Open**作業結束時，物件參考計數會是正確的。  
  
2.  運算式`(_bstr_t)`不是轉換，而是 **_variant_t**運算子，會從**Value**傳回的**variant**中解壓縮 **_bstr_t**的字串。  
  
 運算式`(char*)`不是轉換，而是 **_bstr_t**運算子，會將指標解壓縮到 **_bstr_t**物件中的封裝字串。  
  
 這段程式碼會示範 **_variant_t**和 **_bstr_t**運算子的一些有用行為。  
  
```cpp
// Visual_CPP_ado_prog_4.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr pConn("ADODB.Connection");  
      _RecordsetPtr pRst("ADODB.Recordset");  
  
      pConn->Provider = "sqloledb";  
      pConn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
  
      // Note 1.  
      pRst->Open("authors", _variant_t((IDispatch *) pConn, true), adOpenStatic, adLockReadOnly, adCmdTable);  
      pRst->MoveLast();  
  
      // Note 2.  
      printf("Last name is '%s %s'\n",   
         (char*) ((_bstr_t) pRst->GetFields()->GetItem("au_fname")->GetValue()),  
         (char*) ((_bstr_t) pRst->Fields->Item["au_lname"]->Value));  
  
      pRst->Close();  
      pConn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }     
   ::CoUninitialize();  
}  
```
