---
description: Visual C++ ADO 程式設計
title: Visual C++ ADO 程式設計 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a2e0284db09672d0e92bb952c9e122a65cb8350b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991829"
---
# <a name="visual-c-ado-programming"></a>Visual C++ ADO 程式設計
ADO API 參考描述 ADO 應用程式開發介面的功能 (API) 使用類似 Microsoft Visual Basic 的語法。 雖然預期的物件是所有使用者，但 ADO 程式設計人員採用不同的語言，例如 Visual Basic、Visual C++ (，不論是否有 **#import** 指示詞) ，以及 ADO/WFC 類別封裝 (的 Visual j + +) 。  

> [!NOTE]
> Microsoft 已結束支援2004中的 Visual c + +。

 為了因應這項多樣性， [Visual C++ 語法索引的 ADO](./using-ado-with-microsoft-visual-c.md) 會提供 Visual C++ 的語言特定語法，其中包含 API 參考中功能、參數、例外行為等的一般描述連結。  
  
 ADO 是使用 COM (元件物件模型) 介面所執行。 不過，程式設計人員可以更輕鬆地使用某些程式設計語言中的 COM，而非其他程式設計語言。 例如，幾乎所有使用 COM 的詳細資料都是以隱含方式針對 Visual Basic 程式設計人員處理，而 Visual C++ 程式設計人員必須親自參與這些細節。  
  
 下列各節摘要說明使用 ADO 和 **#import** 指示詞之 c 和 c + + 程式設計人員的詳細資料。 它著重于 COM (**Variant**、 **BSTR**和 **SafeArray**) 的特定資料類型，以及 (_com_error) 的錯誤處理。  
  
## <a name="using-the-import-compiler-directive"></a>使用 #import 編譯器指示詞  
 **#Import** Visual C++ 編譯器指示詞可簡化處理 ADO 方法和屬性。 指示詞會採用包含類型程式庫的檔案名，例如 ( # A0) ，然後產生包含 typedef 宣告的標頭檔、介面的智慧型指標，以及列舉的常數。 每個介面都會封裝或包裝在類別中。  
  
 針對類別中的每個作業 (也就是方法或屬性呼叫) ，會有一個宣告可直接呼叫作業 (也就是作業) 的「原始」形式，以及呼叫原始作業的宣告，如果作業無法順利執行，則會擲回 COM 錯誤。 如果作業是屬性，通常會有一個編譯器指示詞，它會為具有類似 Visual Basic 語法的作業建立替代語法。  
  
 取得屬性值的作業會有格式的名稱： **Get**_屬性_。 設定屬性值的作業具有表單、 **Put**_屬性_的名稱。 使用 ADO 物件的指標設定屬性值的作業具有 **PutRef**_屬性_的格式名稱。  
  
 您可以使用下列形式的呼叫來取得或設定屬性：  
  
```cpp
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```
  
## <a name="using-property-directives"></a>使用屬性指示詞  
 **__Declspec (屬性 ... ) **編譯器指示詞是 Microsoft 專有的 C 語言延伸模組，它會宣告用來作為屬性的函式，以具有替代語法。 如此一來，您就可以使用類似于 Visual Basic 的方式來設定或取得屬性的值。 例如，您可以透過這種方式來設定和取得屬性：  
  
```cpp
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```
  
 請注意，您不需要撰寫程式碼：  
  
```cpp
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```
  
 編譯器會根據所宣告的**Get** _-_ 替代語法以及是否正在讀取或寫入屬性，產生適當的 Get、 **Put**或**PutRef**_屬性_呼叫。  
  
 **__Declspec (屬性 ... ) **編譯器指示詞只能宣告函數的**get**、 **put**或**get**和**put**替代語法。 唯讀作業只有 **get** 宣告;僅限寫入作業只有 **put** 宣告;同時為讀取和寫入的作業都有 **get** 和 **put** 宣告。  
  
 此指示詞只可有兩個宣告：不過，每個屬性都可能有三個屬性函式： **Get**_屬性_、 **Put**_屬性_和 **PutRef**_屬性_。 在此情況下，只有兩種形式的屬性具有替代語法。  
  
 例如， **命令** 物件 **ActiveConnection** 屬性是使用 **Get**_ActiveConnection_ 和 **PutRef**_ActiveConnection_的替代語法來宣告。 **PutRef**語法是不錯的選擇，因為在實務上，您通常會想要將開啟的**連接**物件 (也就是在這個屬性中) 的**連接**物件指標。 另一方面， **Recordset** 物件具有 **Get**、 **Put**和 **PutRef**_ActiveConnection_ 作業，但沒有替代語法。  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>集合、GetItem 方法和 Item 屬性  

 ADO 定義了數個集合，包括 **欄位**、 **參數**、 **屬性**和 **錯誤**。 在 Visual C++ 中， **GetItem (_index_) ** 方法會傳回集合的成員。 *Index* 是 **Variant**，其值是集合中成員的數值索引，或是包含成員名稱的字串。  
  
 **__Declspec (屬性 ... ) **編譯器指示詞會將**Item**屬性宣告為每個集合的基本**GetItem ( # B3**方法的替代語法。 替代語法使用方括弧，看起來類似于陣列參考。 一般而言，這兩種表單看起來會像下面這樣：  
  
```cpp
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```
  
 例如，將值指派給名為**_rs_** 的**記錄集**物件的欄位，該物件會衍生自**pubs**資料庫的**作者**資料表。 使用** ( # B1**屬性的專案來存取**記錄集**物件**欄位**集合的第三個**欄位**， (集合是從零開始編制索引;假設第三個欄位名稱為**_au \_ fname_**) 。 然後呼叫**欄位**物件上** ( # B1**方法的值，以指派字串值。  
  
 這可透過下列四種方式以 Visual Basic 表示， (最後兩個表單對 Visual Basic 而言是唯一的;其他語言沒有對等的) ：  
  
```cpp
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```
  
 上述前兩個表單 Visual C++ 中的對等專案為：  
  
```cpp
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```
  
 -或- (也會顯示 [ **值** ] 屬性的替代語法)   
  
```cpp
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```
  
 如需逐一查看集合的範例，請參閱「ADO 參考」的「ADO 集合」一節。  
  
## <a name="com-specific-data-types"></a>COM 特定的資料類型  
 一般而言，您在 ADO API 參考中找到的任何 Visual Basic 資料類型都有 Visual C++ 對等專案。 這些包括標準資料類型，例如 Visual Basic ** ****位元組**的不**帶正負**號的 char、**整數**的**縮寫** **，以及 long long。** 查看語法 Indexesto 查看指定方法或屬性之運算元的確切需求。  
  
 這項規則的例外狀況是 COM 的特定資料類型： **Variant**、 **BSTR**和 **SafeArray**。  
  
### <a name="variant"></a>變數  
 **Variant**是包含值成員和資料類型成員的結構化資料型別。 **Variant**可能包含各種其他資料類型，包括另一個 VARIANT、BSTR、Boolean、IDispatch 或 IUnknown 指標、currency、date 等等。 COM 也提供可讓您輕鬆地將資料類型轉換成另一種資料類型的方法。  
  
 **_Variant_t**類別會封裝和管理**variant**資料類型。  
  
 當 ADO API 參考指出方法或屬性運算元接受值時，通常表示此值會傳入 **_variant_t**中。  
  
 當 ADO API 參考主題中的 **參數** 區段指出運算元是 **變異變數**時，此規則會明確成立。 其中一個例外狀況是當檔明確指出運算元採用標準資料類型時，例如 **Long** 或 **Byte**或列舉。 另一個例外狀況是當運算元接受 **字串**時。  
  
### <a name="bstr"></a>BSTR  
 **BSTR** (**B**asic **STR**) 是一種結構化資料類型，其中包含字元字串和字串的長度。 COM 提供方法來配置、操作和釋放 **BSTR**。  
  
 **_Bstr_t**類別會封裝和管理**bstr**資料類型。  
  
 當 ADO API 參考指出方法或屬性接受 **字串** 值時，表示值是 **_bstr_t**形式。  
  
### <a name="casting-_variant_t-and-_bstr_t-classes"></a>轉換 _variant_t 和 _bstr_t 類別  
 通常不需要在作業的引數中明確撰寫 **_variant_t** 或 **_bstr_t** 的程式碼。 如果 **_variant_t** 或 **_bstr_t** 類別具有符合引數資料類型的函式，則編譯器會產生適當的 **_variant_t** 或 **_bstr_t**。  
  
 但是，如果引數不明確，也就是引數的資料類型符合一個以上的函式，您必須使用適當的資料類型來轉換引數，以叫用正確的函式。  
  
 例如， **記錄集：： Open** 方法的宣告為：  
  
```cpp
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```
  
 `ActiveConnection`引數會使用 **_variant_t**的參考，您可以將其編碼為連接字串或開啟**連接**物件的指標。  
  
 如果您 **_variant_t**傳遞字串（例如 " `DSN=pubs;uid=MyUserName;pwd=MyPassword;` "）或指標（例如 ""），則會隱含地建立正確的 _variant_t `(IDispatch *) pConn` 。  
  
> [!NOTE]
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在連接字串中指定 **Trusted_Connection = yes** 或 **整合式安全性 = SSPI** ，而不是使用者識別碼和密碼資訊。  
  
 或者，您可以明確編碼包含指標的 **_variant_t** ，例如 " `_variant_t((IDispatch *) pConn, true)` "。 `(IDispatch *)`轉型會以另一個接受 IUnknown 介面指標的函式來解析混淆。  
  
 這一點很重要，但很少提到，ADO 是 IDispatch 介面。 每當 ADO 物件的指標都必須以 **變異**形式傳遞時，該指標就必須轉換為 IDispatch 介面的指標。  
  
 最後一個案例會明確地以其選擇性的預設值來為函式的第二個布林值引數進行編碼 `true` 。 這個引數會讓 **Variant** 函式呼叫其 **AddRef** ( # A1 方法，它會在 ado 方法或屬性呼叫完成時，補償 ado 自動呼叫 **_variant_t：： Release** ( # A3 方法。  
  
### <a name="safearray"></a>SafeArray  
 **SafeArray**是結構化資料類型，其中包含其他資料類型的陣列。 **SafeArray**稱為*安全*的，因為它包含每個陣列維度之界限的相關資訊，並限制對這些界限內陣列元素的存取。  
  
 當 ADO API 參考指出方法或屬性接受或傳回陣列時，表示方法或屬性會接受或傳回 **SafeArray**，而不是原生 C/c + + 陣列。  
  
 例如， **連接** 物件 **OpenSchema** 方法的第二個參數需要 **Variant** 值的陣列。 這些 **變數** 值必須傳遞為 **SafeArray**的元素，而且必須將該 **Safearray** 設定為另一個 **Variant**的值。 它是以**OpenSchema**的第二個引數形式傳遞的其他**變異**。  
  
 在進一步的範例中， **Find**方法的第一個引數是值為一維**SafeArray**的**Variant** ;**AddNew**的每個選擇性第一個和第二個引數是一維**SafeArray**;而**GetRows**方法的傳回值是一種**Variant** ，其值為二維的**SafeArray**。  
  
## <a name="missing-and-default-parameters"></a>遺漏和預設參數  
 Visual Basic 允許方法中遺漏參數。 例如， **Recordset** 物件 **Open** 方法有五個參數，但您可以略過中繼參數，並省略尾端參數。 根據遺漏運算元的資料類型，將會取代預設的 **BSTR** 或 **變異** 數。  
  
 在 C/c + + 中，必須指定所有的運算元。 如果您想要指定其資料類型是字串的遺漏參數，請指定包含 null 字串的 **_bstr_t** 。 如果您想要指定其資料類型為 **Variant**的遺漏參數，請指定具有 DISP_E_PARAMNOTFOUND 值和 VT_ERROR 類型的 **_variant_t** 。 或者，指定 **#import**指示詞提供的對等 **_variant_t**常數**vtMissing**。  
  
 一般使用 **vtMissing**時，有三種方法是例外狀況。 這些是**連接**和**命令**物件的**Execute**方法，以及**記錄集**物件的**NextRecordset**方法。 以下是其簽章：  
  
```cpp
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```
  
 參數（ *RecordsAffected* 和 *參數*）是 **Variant**的指標。 *參數* 是輸入參數，可指定包含單一參數或參數陣列的 Variant 位址，這些 **變數** 將會修改執行的命令。 *RecordsAffected* 是一個輸出參數，可指定 **Variant**的位址，其中會傳回受方法影響的資料列數目。  
  
 在 **命令** 物件 **執行** 方法中，藉由將 *參數* 設定為 `&vtMissing` (建議) 或 null 指標 (也就是 **null** 或零 (0) # A5，指出未指定任何參數。 如果 *參數* 設定為 null 指標，則此方法會在內部替代 **vtMissing**的對等專案，然後完成此作業。  
  
 在所有方法中，將 *RecordsAffected* 設定為 null 指標，表示不應傳回受影響的記錄數目。 在此情況下，null 指標不會有太多遺漏的參數，因為這表示方法應該捨棄受影響的記錄數目。  
  
 因此，這三種方法的程式碼如下：  
  
```cpp
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```
  
## <a name="error-handling"></a>錯誤處理  
 在 COM 中，大部分的作業會傳回 HRESULT 傳回碼，指出函式是否已順利完成。 **#Import**指示詞會針對每個「原始」方法或屬性來產生包裝函式程式碼，並檢查傳回的 HRESULT。 如果 HRESULT 指出失敗，包裝函式程式碼會藉由以 HRESULT 傳回碼作為引數來呼叫 _com_issue_errorex ( # A1 來擲回 COM 錯誤。 COM 錯誤物件可以在**try** - **catch**區塊中捕捉。  (為了提高效率，請攔截 **_com_error** 物件的參考。 )   
  
 請記住，這些是 ADO 錯誤：由於 ADO 作業失敗所造成。 基礎提供者所傳回的錯誤會在**連接**物件**錯誤**集合中顯示為**錯誤**物件。  
  
 **#Import**指示詞只會針對在 ADO 中宣告的方法和屬性建立錯誤處理常式。 不過，您可以藉由撰寫自己的錯誤檢查宏或內嵌函式，來利用這個相同的錯誤處理機制。 如需範例，請參閱下列各節中的主題、 [Visual C++ 擴充](./visual-c-extensions-for-ado.md)功能或程式碼。  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Visual C++ Visual Basic 慣例的對應專案  
 以下是 ADO 檔中數個慣例的摘要，在 Visual Basic 中撰寫程式碼，以及 Visual C++ 中的對應專案。  
  
### <a name="declaring-an-ado-object"></a>宣告 ADO 物件  
 在 Visual Basic 中，在此案例中， (**記錄集** 物件) 的 ADO 物件變數會宣告如下：  
  
```vb
Dim rst As ADODB.Recordset  
```
  
 子句（" `ADODB.Recordset` "）是在登錄中定義之 **記錄集** 物件的 ProgID。 **記錄**物件的新實例會宣告如下：  
  
```vb
Dim rst As New ADODB.Recordset  
```
  
 -或-  
  
```vb
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```
  
 在 Visual C++ 中， **#import** 指示詞會產生所有 ADO 物件的智慧型指標類型宣告。 例如，指向 **_Recordset** 物件的變數屬於 **_RecordsetPtr**類型，並宣告如下：  
  
```cpp
_RecordsetPtr  rs;  
```
  
 指向 **_Recordset** 物件新實例的變數宣告如下：  
  
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
  
 在呼叫 **CreateInstance** 方法之後，可以使用變數，如下所示：  
  
```cpp
rs->Open(...);  
```
  
 請注意，在一個情況下， `.` 會使用 "" 運算子，如同變數是類別 () 的實例， `rs.CreateInstance` 而在另一個情況下，則 `->` 會使用 "" 運算子，如同變數是指向介面的指標 (`rs->Open`) 。  
  
 有兩種方式可以使用一個變數，因為 " `->` " 運算子已多載，以便讓類別的實例能夠像介面指標一樣運作。 執行個體變數的私用類別成員包含 **_Recordset** 介面的指標;" `->` " 運算子會傳回該指標，而傳回的指標會存取 **_Recordset** 物件的成員。  
  
### <a name="coding-a-missing-parameter---string"></a>編寫遺漏參數字串的程式碼  
 當您需要在 Visual Basic 中撰寫遺漏 **字串** 運算元的程式碼時，只會省略運算元。 您必須在 Visual C++ 中指定運算元。 編寫 **_bstr_t** ，其具有空字串作為值。  
  
```cpp
_bstr_t strMissing(L"");  
```
  
### <a name="coding-a-missing-parameter---variant"></a>為遺漏的參數撰寫程式碼-Variant  
 當您需要在 Visual Basic 中撰寫遺漏的 **變異** 運算元的程式碼時，只會省略運算元。 您必須在 Visual C++ 中指定所有的運算元。 使用 **_variant_t**設定為特殊值、DISP_E_PARAMNOTFOUND 和類型 VT_ERROR 來撰寫遺漏**變異**參數的程式碼。 或者，指定 **vtMissing**，這是 **#import** 指示詞所提供的相等預先定義常數。  
  
```cpp
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```
  
 -或使用-  
  
```cpp
...vtMissing...;  
```
  
### <a name="declaring-a-variant"></a>宣告變異  
 在 Visual Basic 中， **變數** 會以 **Dim** 語句宣告，如下所示：  
  
```vb
Dim VariableName As Variant  
```
  
 在 Visual C++ 中，將變數宣告為類型 **_variant_t**。 以下顯示一些示意圖 **_variant_t** 宣告。  
  
> [!NOTE]
>  這些宣告只會對您在自己的程式中撰寫程式碼的概念有大致的瞭解。 如需詳細資訊，請參閱下列範例和 Visual C + + 檔。  
  
```cpp
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```
  
### <a name="using-arrays-of-variants"></a>使用 Variant 陣列  
 在 Visual Basic 中，您可以使用**Dim**語句來撰寫**變數**陣列的程式碼，或者，您可以使用**陣列**函式，如下列範例程式碼所示：  
  
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
  
 下列 Visual C++ 範例示範如何使用與 **_variant_t**搭配使用的**SafeArray** 。  
  
#### <a name="notes"></a>注意  
 下列附注對應到程式碼範例中的批註區段。  
  
1.  同樣地，TESTHR ( # A1 內嵌函式定義為利用現有的錯誤處理機制。  
  
2.  您只需要一維陣列，因此您可以使用 **SafeArrayCreateVector**，而不是一般用途的 **SAFEARRAYBOUND** 宣告和 **SafeArrayCreate** 函數。 以下是該程式碼使用 **SafeArrayCreate**時的樣子：  
  
    ```cpp
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```
  
3.  列舉常數 **adSchemaColumns**所識別的架構與四個條件約束資料行相關聯： TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME 和 COLUMN_NAME。 因此，會建立具有四個元素的 **Variant** 值陣列。 然後，會指定對應至第三個數據行（TABLE_NAME）的條件約束值。  
  
     傳回的 **記錄集會** 包含數個數據行，其中的子集是條件約束資料行。 每個傳回資料列的條件約束資料行值，必須與對應的條件約束值相同。  
  
4.  熟悉 **safearray** 的人可能會驚訝，因為 **SafeArrayDestroy** ( # A1 不會在結束之前呼叫。 事實上，在此情況下呼叫 **SafeArrayDestroy** ( # A1 會導致執行時間例外狀況。 原因是， `vtCriteria` 當 **_variant_t**超出範圍（可釋放**SafeArray**）時，的的函式會呼叫**VariantClear** ( # A1。 呼叫 **SafeArrayDestroy**，而不以手動方式清除 **_variant_t**，會導致該函式嘗試清除不正確 **SafeArray** 指標。  
  
     如果呼叫 **SafeArrayDestroy** ，程式碼看起來會像這樣：  
  
    ```cpp
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```
  
     不過，讓 **_variant_t** 管理 **SafeArray**更為簡單。  
  
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
  
### <a name="using-property-getputputref"></a>使用 Property Get/Put/PutRef  
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
  
 此 Visual C++ 範例示範**Get** / **Put** / **PutRef**_屬性_。  
  
#### <a name="notes"></a>注意  
 下列附注對應到程式碼範例中的批註區段。  
  
1.  這個範例會使用兩種形式的遺漏字串引數：明確的常數、 **strMissing**，以及編譯器將用來建立**開啟**方法範圍所存在之暫時 **_bstr_t**的字串。  
  
2.  不需要將運算元轉換 `rs->PutRefActiveConnection(cn)` 為， `(IDispatch *)` 因為運算元的類型已經存在 `(IDispatch *)` 。  
  
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
  
### <a name="using-getitemx-and-itemx"></a>使用 GetItem (x) 和專案 [x]  
 此 Visual Basic 範例示範 ( # A1 **專案** 的標準和替代語法。  
  
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
  
 此 Visual C++ 範例示範 **專案**。  
  
> [!NOTE]
>  下列附注對應于程式碼範例中的批註區段：當使用 **專案**存取集合時，索引 **2**必須轉換為 **long** ，才能叫用適當的函式。  
  
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
  
### <a name="casting-ado-object-pointers-with-idispatch-"></a>使用 (IDispatch * ) 轉換 ADO 物件指標  
 下列 Visual C++ 範例將示範如何使用 (IDispatch * ) 來轉換 ADO 物件指標。  
  
#### <a name="notes"></a>注意  
 下列附注對應到程式碼範例中的批註區段。  
  
1.  以明確編碼的**Variant**指定開啟的**連接**物件。 將其轉換為 (IDispatch \*) ，以便叫用正確的函式。 此外，請將第二個 **_variant_t** 參數明確設定為預設值 **true**，因此當 **Recordset：： Open** 作業結束時，物件參考計數將會是正確的。  
  
2.  運算式不是轉 `(_bstr_t)` 型，而是 **_variant_t**運算子，可從**值**傳回的**變數**中解壓縮 **_bstr_t**字串。  
  
 運算式不是 `(char*)` cast，而是 **_bstr_t** 運算子，可將指標解壓縮至 **_bstr_t** 物件中的封裝字串。  
  
 這一節的程式碼示範 **_variant_t** 和 **_bstr_t** 運算子的一些有用行為。  
  
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