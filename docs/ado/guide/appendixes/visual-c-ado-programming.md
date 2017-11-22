---
title: "Visual c + + ADO 程式設計 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO]
ms.assetid: 11233b96-e05c-4221-9aed-5f20944b0f1c
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8decc959840898d0b82c86c0d955b29a7affddde
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="visual-c-ado-programming"></a>Visual c + + ADO 程式設計
ADO 應用程式開發介面參考描述 ADO 應用程式開發介面 (API) 的語法以 Microsoft Visual Basic 類似的功能。 適用對象是所有使用者，雖然 ADO 程式設計人員採用各種不同的語言，例如 Visual Basic、 Visual c + + (逾時或無**#import**指示詞)，和 Visual J + + （與 ADO/WFC 類別封裝）。  

> [!NOTE]
> Microsoft 在 2004 年結束支援的 Visual J + +。

 若要容納這些多樣性， [Visual c + + 語法索引 ADO](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) Visual c + + 語言特定語法提供的功能、 參數、 異常行為和等等，API 中的一般說明連結參考。  
  
 ADO 是使用 COM （元件物件模型） 介面實作。 不過，它是比其他某些程式設計語言中使用 COM 的程式設計人員更容易。 比方說，使用 COM 的幾乎所有詳細資料以隱含方式針對處理 Visual Basic 程式設計人員，而 Visual c + + 程式設計人員都必須參加本身這些詳細資料。  
  
 下列各節摘要詳細資料的 C 和 c + + 程式設計人員使用 ADO 和**#import**指示詞。 它著重在特定 COM 的資料型別 (**Variant**， **BSTR**，和**SafeArray**)，和錯誤處理 (_com_error)。  
  
## <a name="using-the-import-compiler-directive"></a>使用 #import 編譯器指示詞  
 **#Import** Visual c + + 編譯器指示詞可簡化使用 ADO 方法和屬性。 指示詞會採用包含類型程式庫，例如 ADO.dll (Msado15.dll)，檔案名稱，並產生包含 typedef 宣告、 介面和列舉的常數的智慧型指標的標頭檔。 封裝或包裝，類別中的每個介面。  
  
 每個作業內的類別 （也就是方法或屬性呼叫），也無需來呼叫作業直接 （也就是 「 原始 」 形式的作業），在宣告呼叫未經處理的作業，並擲回 COM 錯誤，如果作業無法執行 succ 宣告essfully。 如果作業是屬性，所以通常建立的 Visual Basic 語法的操作替代語法的編譯器指示詞。  
  
 擷取屬性值的作業有的名稱格式，**取得***屬性*。 設定屬性值的作業有的名稱格式，**放***屬性*。 具有指標的屬性值設定為 ADO 物件的作業有的名稱格式， **PutRef***屬性*。  
  
 您可以取得或設定具有呼叫種形式的屬性：  
  
```  
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```  
  
## <a name="using-property-directives"></a>使用屬性指示詞  
 **__Declspec(property...)**編譯器指示詞是 Microsoft 專有 C 語言擴充功能，將函式宣告為屬性用來替代的語法。 如此一來，您可以設定或取得屬性值的方式類似於 Visual Basic。 例如，您可以設定，而這種方式取得的屬性：  
  
```  
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```  
  
 請注意您不會有程式碼：  
  
```  
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```  
  
 編譯器會產生適當**取得***-*，**放**-，或**PutRef***屬性*呼叫根據哪些替代語法宣告和屬性是否正在讀取或寫入。  
  
 **__Declspec(property...)**編譯器指示詞只可以宣告**取得**，**放**，或**取得**和**放**函式的替代語法。 唯讀作業只能有**取得**宣告; 唯寫的作業只能有**放**宣告; 作業都讀取及寫入同時具有**取得**和**放**宣告。  
  
 只能使用兩個宣告具有此指示詞。不過，每一個屬性可能有三個屬性函式：**取得***屬性*，**放***屬性*，和**PutRef***屬性*。 在此情況下，只有兩種形式的屬性有替代語法。  
  
 例如，**命令**物件**ActiveConnection**屬性宣告的替代語法與**取得***ActiveConnection*和**PutRef***ActiveConnection*。 **PutRef**-的語法是不錯的選擇，因為在實務上，您通常想要將開啟**連接**物件 (也就是**連接**物件指標) 在此屬性。 相反地，**資料錄集**物件具有**取得**-，**放**-，以及**PutRef***ActiveConnection*作業，但沒有替代的語法。  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>集合、 GetItem 方法中，與項目屬性  
 ADO 定義數個集合，包括**欄位**，**參數**，**屬性**，和**錯誤**。 Visual c + + **GetItem (***索引***)**方法會傳回集合的成員。 *索引*是**Variant**，其值為集合中成員的數值索引或字串，包含成員的名稱。  
  
 **__Declspec(property...)**編譯器指示詞宣告**項目**作為替代語法，加入每一個集合屬性的基本**GetItem()**方法。 替代語法會使用方括號，並尋找類似陣列參考。 一般情況下，兩種形式如下所示：  
  
```  
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```  
  
 例如，將值指派給欄位的**資料錄集**物件，名為***rs***、 衍生自**作者**資料表**pubs**資料庫。 使用**m （)**屬性來存取第三個**欄位**的**資料錄集**物件**欄位**集合 （集合編排索引零，假設名為第三個欄位***au_fname***)。 然後呼叫**value （)**方法**欄位**指定字串值的物件。  
  
 這可在 Visual Basic 中以表示下列四種方法 （Visual basic 特有的最後兩個表單; 其他語言並沒有對等項目）：  
  
```  
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```  
  
 在 Visual c + + 中相當於上面的前兩個表單是：  
  
```  
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```  
  
 -(替代語法**值**屬性也會顯示)  
  
```  
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```  
  
 如需逐一查看集合的範例，請參閱 < ADO 參考 > 的 「 ADO 集合 」 一節。  
  
## <a name="com-specific-data-types"></a>COM 特定資料類型  
 一般情況下，您在 ADO 應用程式開發介面參考中找到任何 Visual Basic 資料型別具有相等 Visual c + +。 這包括標準的資料類型，例如**unsigned char**適用於 Visual Basic**位元組**，**簡短**如**整數**，和**長**如**長**。 查詢語法 Indexesto 中的看到完全所需內容的指定的方法或屬性的運算元。  
  
 此規則的例外狀況是 COM 的特定資料型別： **Variant**， **BSTR**，和**SafeArray**。  
  
### <a name="variant"></a>變數  
 A **Variant**是結構化的資料類型，其中包含值成員和資料型別成員。 A **Variant**可能包含各種不同的其他資料類型，包括另一個變數、 BSTR、 布林值、 IDispatch 或 IUnknown 指標、 貨幣、 日期和等等。 COM 也提供了可讓您輕鬆的方法會將一種資料類型轉換到另一個。  
  
 **_Variant_t**類別會封裝並管理**Variant**資料型別。  
  
 當 ADO 應用程式開發介面參考指出方法或屬性運算元接受值時，通常表示的值會傳遞**_variant_t**。  
  
 此規則時，會明確情況**參數**部分 ADO 應用程式開發介面參考主題中的說明的運算元會以**Variant**。 其中一個例外是當文件明確表示運算元採用標準資料型別，例如**長**或**位元組**，或列舉型別。 另一個例外狀況就是當運算元採取**字串**。  
  
### <a name="bstr"></a>BSTR  
 A **BSTR** (**B**rswindowsbasic **STR**ing) 是結構化的資料類型，其中包含的字元字串和字串的長度。 COM 提供方法來配置、 操作及釋放**BSTR**。  
  
 **_Bstr_t**類別會封裝並管理**BSTR**資料型別。  
  
 ADO 應用程式開發介面參考時顯示方法或屬性會採用**字串**值，就表示值的形式**_bstr_t**。  
  
### <a name="casting-variantt-and-bstrt-classes"></a>轉型 _variant_t 和 _bstr_t 類別  
 通常不需要明確的程式碼**_variant_t**或**_bstr_t**中作業的引數。 如果**_variant_t**或**_bstr_t**類別具有比對引數的資料類型的建構函式，編譯器會產生適當**_variant_t**或**_bstr_t**。  
  
 不過，如果引數是模稜兩可，也就是引數的資料類型符合一個以上的建構函式中，您必須與要叫用正確的建構函式的適當資料類型轉換的引數。  
  
 例如，宣告**Recordset::Open**方法是：  
  
```  
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```  
  
 `ActiveConnection`引數會參考**_variant_t**，您可能會為連接字串或是指向已開啟的程式碼**連接**物件。  
  
 正確**_variant_t**如果您傳遞字串，例如隱含建構"`DSN=pubs;uid=MyUserName;pwd=MyPassword;`"，或資料指標，例如"`(IDispatch *) pConn`"。  
  
> [!NOTE]
>  如果您要連接至資料來源提供者支援 Windows 驗證，您應該指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是使用者識別碼和密碼連接字串中的資訊。  
  
 您可能會明確地撰寫程式碼或**_variant_t**包含指標，例如"`_variant_t((IDispatch *) pConn, true)`"。 轉型， `(IDispatch *)`，解析以接受 IUnknown 介面指標的另一個建構函式模稜兩可。  
  
 雖然很少提及 ADO 是 IDispatch 介面的事實，相當重要。 每當必須傳遞 ADO 物件的指標為**Variant**，該指標必須轉換成的 IDispatch 介面的指標。  
  
 最後一個案例明確代碼的第二個布林引數的建構函式其選擇性的預設值是`true`。 這個引數會導致**Variant**建構函式來呼叫其**AddRef**（） 方法，會自動呼叫 ADO 補償**_variant_t::Release**（） 方法ADO 方法或屬性呼叫完成的時間。  
  
### <a name="safearray"></a>SafeArray  
 A **SafeArray**是結構化的資料類型，其中包含其他資料類型的陣列。 A **SafeArray**稱為*安全*因為它包含每個陣列維度的界限資訊，並限制存取陣列項目，這些範圍內。  
  
 當 ADO 應用程式開發介面參考指出方法或屬性會使用或傳回陣列，表示方法或屬性接受或傳回**SafeArray**，不原生 C/c + + 陣列。  
  
 例如，第二個參數**連接**物件**OpenSchema**方法需要的陣列**Variant**值。 這些**Variant**必須傳遞值的項目為**SafeArray**，而且**SafeArray**必須設定為另一個值**Variant**. 它是其他**Variant**做為第二個引數傳遞**OpenSchema**。  
  
 為進一步範例中，第一個引數**尋找**方法**Variant**其值是一維**SafeArray**; 每個選擇性的第一個和第二個引數**AddNew**是一維**SafeArray**; 和傳回值**GetRows**方法**Variant**其值是二維**SafeArray**。  
  
## <a name="missing-and-default-parameters"></a>遺失，且預設參數  
 Visual Basic 允許遺漏的方法中的參數。 例如，**資料錄集**物件**開啟**方法有五個參數，但您可以略過中繼參數和離開句尾參數。 預設值**BSTR**或**Variant**將取代根據遺漏運算元的資料類型。  
  
 C/c + +，您必須指定所有的運算元。 如果您想要指定遺失參數的資料類型是字串，指定**_bstr_t**包含 null 字串。 如果您想要指定遺失參數的資料型別**Variant**，指定**_variant_t** DISP_E_PARAMNOTFOUND 且類型為 VT_ERROR 的值。 或者，指定對等項目**_variant_t**常數， **vtMissing**，這由所提供**#import**指示詞。  
  
 三種方法全都例外狀況的一般用法的**vtMissing**。 這些是**Execute**方法**連接**和**命令**物件，而**NextRecordset**方法**資料錄集**物件。 以下是其簽章：  
  
```  
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```  
  
 參數， *RecordsAffected*和*參數*，是指向**Variant**。 *參數*為輸入的參數會指定的位址**Variant**包含單一參數或參數，將會修改正在執行的命令的陣列。 *RecordsAffected*是一個 output 參數，指定的位址**Variant**，其中傳回的方法所影響的資料列數目。  
  
 在**命令**物件**Execute**方法，表示未指定任何參數，藉由設定*參數*為`&vtMissing`（這建議選項） 或null 指標 (也就是**NULL**或零 (0))。 如果*參數*設定 null 指標，該方法在內部替代的對等**vtMissing**，然後完成此作業。  
  
 在所有方法，會指出受影響的記錄數目不會傳回藉由設定*RecordsAffected* null 指標。 在此情況下，null 指標不是很多，所以遺漏參數做為此方法應該捨棄受影響的記錄數目表示。  
  
 因此，這三種方法，如它是有效的項目這類程式碼：  
  
```  
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```  
  
## <a name="error-handling"></a>錯誤處理  
 在 COM 中，大部分的作業會傳回 HRESULT 傳回碼指出函數是否已順利完成。 **#Import**指示詞會產生包裝函式程式碼，每個 「 原始 」 的方法或屬性，並檢查傳回的 HRESULT。 如果 HRESULT 指出失敗，包裝函式程式碼會擲回 COM 錯誤的 HRESULT 傳回碼的呼叫 _com_issue_errorex() 做為引數。 可以攔截 COM 錯誤物件，於**再試一次**-**攔截**區塊。 (如效率的因素，攔截的參考**_com_error**物件。)  
  
 請記住，這些是 ADO 錯誤： 它們會從 ADO 作業失敗。 基礎提供者所傳回的錯誤會顯示為**錯誤**中的物件**連接**物件**錯誤**集合。  
  
 **#Import**指示詞建立只有錯誤處理常式方法和 ADO.dll 中宣告的屬性。 不過，您也可以利用這個相同的錯誤處理機制，藉由撰寫您自己的錯誤檢查巨集或內嵌函式。 請參閱主題 < [Visual c + + 擴充功能](../../../ado/guide/appendixes/visual-c-extensions-for-ado.md)，或在下列各節，如需範例程式碼。  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Visual Basic 慣例的 visual c + + 對等項目  
 以下是幾個 ADO 文件、 自動程式碼在 Visual Basic 及 Visual c + + 中的對應項慣例的摘要。  
  
### <a name="declaring-an-ado-object"></a>宣告 ADO 物件  
 在 Visual Basic，ADO 物件變數 (在此情況下，如**資料錄集**物件) 的宣告如下：  
  
```  
Dim rst As ADODB.Recordset  
```  
  
 在子句中，「`ADODB.Recordset`」，是的 ProgID**資料錄集**登錄中所定義的物件。 新執行個體**記錄**物件宣告，如下所示：  
  
```  
Dim rst As New ADODB.Recordset  
```  
  
 -或-  
  
```  
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```  
  
 Visual c + + **#import**指示詞會產生所有 ADO 物件的智慧型指標類型宣告。 比方說，此變數會指向**_Recordset**物件屬於類型**_RecordsetPtr**，並宣告，如下所示：  
  
```  
_RecordsetPtr  rs;  
```  
  
 新執行個體所指向的變數**_Recordset**物件宣告，如下所示：  
  
```  
_RecordsetPtr  rs("ADODB.Recordset");  
```  
  
 -或-  
  
```  
_RecordsetPtr  rs;  
rs.CreateInstance("ADODB.Recordset");  
```  
  
 -或-  
  
```  
_RecordsetPtr  rs;  
rs.CreateInstance(__uuidof(_Recordset));  
```  
  
 之後**CreateInstance**呼叫方法時，變數可用，如下所示：  
  
```  
rs->Open(...);  
```  
  
 請注意，在其中一個案例中，"`.`"好像變數類別的執行個體使用運算子 (`rs.CreateInstance`)，並在其他情況下，"`->`"如同變數是介面的指標，使用運算子 (`rs->Open`)。  
  
 其中一個變數可以用兩種方式，因為 「`->`"運算子多載之後可允許的作用如同指標至介面的類別執行個體。 私用類別的成員執行個體變數包含的指標**_Recordset**介面;"`->`」 運算子會傳回該指標，並傳回的指標存取成員**_Recordset**物件。  
  
### <a name="coding-a-missing-parameter--string"></a>撰寫程式碼遺失參數-字串  
 當您需要撰寫程式碼遺失**字串**運算元在 Visual Basic 中，您只可以省略運算元。 在 Visual c + + 中，您必須指定的運算元。 程式碼**_bstr_t**具有值為空字串。  
  
```  
_bstr_t strMissing(L"");  
```  
  
### <a name="coding-a-missing-parameter--variant"></a>撰寫程式碼遺失參數-Variant  
 當您需要撰寫程式碼遺失**Variant**運算元在 Visual Basic 中，您只可以省略運算元。 在 Visual c + + 中，您必須指定所有的運算元。 程式碼遺失**Variant**參數**_variant_t**設為特殊值、 DISP_E_PARAMNOTFOUND，且型別，VT_ERROR。 或者，指定**vtMissing**，這對等的預先定義的常數由所提供**#import**指示詞。  
  
```  
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```  
  
 -或使用-  
  
```  
...vtMissing...;  
```  
  
### <a name="declaring-a-variant"></a>宣告變數  
 在 Visual Basic 中**Variant**宣告與**Dim**陳述式，如下所示：  
  
```  
Dim VariableName As Variant  
```  
  
 在 Visual c + + 中，將變數宣告為類型**_variant_t**。 少數的圖解**_variant_t**宣告如下所示。  
  
> [!NOTE]
>  這些宣告只可讓您會撰寫您自己的程式中的粗略想法。 如需詳細資訊，請參閱以下範例中和 Visual C + + 文件。  
  
```  
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```  
  
### <a name="using-arrays-of-variants"></a>使用 Variant 的陣列  
 在 Visual Basic 中的陣列**變異**可以硬式編碼**Dim**陳述式，或者您可能使用**陣列**函式，如下列範例程式碼所示：  
  
```  
Public Sub ArrayOfVariants  
Dim cn As ADODB.Connection  
Dim rs As ADODB.Recordset  
Dim fld As ADODB.Field  
  
    cn.Open "DSN=pubs"  
    rs = cn.OpenSchema(adSchemaColumns, _  
        Array(Empty, Empty, "authors", Empty))  
    For Each fld in rs.Fields  
        Debug.Print "Name = "; fld.Name  
    Next fld  
    rs.Close  
    cn.Close  
End Sub  
```  
  
 下列 Visual c + + 範例示範如何使用**SafeArray**搭配**_variant_t**。  
  
#### <a name="notes"></a>注意  
 下列附註會對應至程式碼範例中加上註解區段。  
  
1.  同樣地，若要善用現有的錯誤處理機制定義 TESTHR() 內嵌函式。  
  
2.  您只需要一維陣列，因此您可以使用**SafeArrayCreateVector**，而不是一般用途**SAFEARRAYBOUND**宣告和**SafeArrayCreate**函式。 以下是該程式碼會看起來使用**SafeArrayCreate**:  
  
    ```  
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```  
  
3.  結構描述所列舉的常數，識別**adSchemaColumns**，都與四個條件約束資料行： table_catalog 排列，TABLE_SCHEMA、 TABLE_NAME、 COLUMN_NAME。 因此，陣列**Variant**建立四個元素的值。 然後指定對應到第三個資料行，TABLE_NAME 的條件約束值。  
  
     **資料錄集**所傳回的是子集的條件約束資料行的數個資料行所組成。 每個傳回的資料列之條件約束資料行的值必須是對應的條件約束值相同。  
  
4.  熟悉**Safearray**可能會感到驚訝， **SafeArrayDestroy**（） 不會在結束前呼叫。 事實上，呼叫**SafeArrayDestroy**（） 在此情況下會造成執行階段例外狀況。 原因在於的解構函式`vtCriteria`會呼叫**Vvalue**（) 時**_variant_t**超出範圍，會釋放**SafeArray**。 呼叫**SafeArrayDestroy**，而不手動清除**_variant_t**，導致嘗試清除不正確的解構函式**SafeArray**指標。  
  
     如果**SafeArrayDestroy**所呼叫，程式碼看起來會像這樣：  
  
    ```  
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```  
  
     不過，很容易讓**_variant_t**管理**SafeArray**。  
  
```  
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
  
### <a name="using-property-getputputref"></a>使用屬性的 Get/Put/PutRef  
 在 Visual Basic 中的屬性名稱是由它擷取、 指派時，是否將參考指派給不限定的。  
  
```  
Public Sub GetPutPutRef  
Dim rs As New ADODB.Recordset  
Dim cn As New ADODB.Connection  
Dim sz as Integer  
cn.Open "Provider=sqloledb;Data Source=yourserver;" & _  
         "Initial Catalog=pubs;Integrated Security=SSPI;"  
rs.PageSize = 10  
sz = rs.PageSize  
rs.ActiveConnection = cn  
rs.Open "authors",,adOpenStatic  
' ...  
rs.Close  
cn.Close  
End Sub  
```  
  
 此 Visual c + + 範例示範**取得**/**放**/**PutRef***屬性*。  
  
#### <a name="notes"></a>注意  
 下列附註會對應至程式碼範例中加上註解區段。  
  
1.  這個範例會使用遺漏的字串引數的兩種： 明確的常數， **strMissing**，和字串編譯器將用來建立暫存**_bstr_t**會存在於範圍的**開啟**方法。  
  
2.  不需要轉換的運算元`rs->PutRefActiveConnection(cn)`至`(IDispatch *)`因為運算元的類型已經`(IDispatch *)`。  
  
```  
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
  
### <a name="using-getitemx-and-itemx"></a>使用 GetItem(x) 和項目 [x]  
 此 Visual Basic 範例示範的標準和替代語法**項目**（)。  
  
```  
Public Sub GetItemItem  
Dim rs As New ADODB.Recordset  
Dim name as String  
rs = rs.Open "authors", "DSN=pubs;", adOpenDynamic, _  
         adLockBatchOptimistic, adTable  
name = rs(0)  
' -or-  
name = rs.Fields.Item(0)  
rs(0) = "Test"  
rs.UpdateBatch  
' Restore name  
rs(0) = name  
rs.UpdateBatch  
rs.Close  
End Sub  
```  
  
 此 Visual c + + 範例示範**項目**。  
  
> [!NOTE]
>  程式碼範例中加上註解區段對應下列附註： 以存取集合時**項目**，索引中， **2**，必須轉換成**長**讓適當的建構函式會叫用。  
  
```  
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
  
### <a name="casting-ado-object-pointers-with-idispatch-"></a>使用 ADO 物件指標轉型 (IDispatch *)  
 下列 Visual c + + 範例示範如何使用 (IDispatch *) 來轉換 ADO 物件指標。  
  
#### <a name="notes"></a>注意  
 下列附註會對應至程式碼範例中加上註解區段。  
  
1.  指定開啟**連接**中明確地自動程式化物件**Variant**。 它與轉換 (IDispatch \*) 讓正確的建構函式會叫用。 此外，明確地設定第二個**_variant_t**參數的預設值來**true**，因此物件參考計數將會是正確時**Recordset::Open**作業就會結束。  
  
2.  運算式， `(_bstr_t)`，不是轉型，但**_variant_t**運算子，它會擷取**_bstr_t**字串從**Variant**傳回**值**.  
  
 運算式， `(char*)`，不是轉型，但**_bstr_t**運算子，它會擷取在封裝的字串指標**_bstr_t**物件。  
  
 這段程式碼示範一些有用的行為**_variant_t**和**_bstr_t**運算子。  
  
```  
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
