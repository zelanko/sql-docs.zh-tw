---
title: HelloData 上的批註 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hellodata sample application [ADO]
ms.assetid: a2831d77-7040-4b73-bbae-fe0bf78107ed
author: rothja
ms.author: jroth
ms.openlocfilehash: 3836d577ab9230e425f42a52b53ed82d3354d72a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761174"
---
# <a name="comments-on-hellodata"></a>HelloData 的註解
HelloData 應用程式會逐步解說一般 ADO 應用程式的基本作業：取得、檢查、編輯和更新資料。 當您啟動應用程式時，請按一下第一個按鈕 [**取得資料**]。 這會**執行 [，** ] 副程式。  
  
## <a name="getdata"></a>GetData  
 [參數] 會將有效的連接**字串放入**模組層級變數中， *m_sConnStr*。 如需連接字串的詳細資訊，請參閱[建立連接字串](../../../ado/guide/data/creating-a-connection-string.md)。  
  
 使用 Visual Basic **OnError**語句來指派錯誤處理常式。 如需 ADO 中錯誤處理的詳細資訊，請參閱[錯誤處理](../../../ado/guide/data/error-handling.md)。 隨即建立新的**連接**物件，而且**CursorLocation**屬性會設定為**adUseClient** ，因為 HelloData 範例會建立*中斷連接的記錄集*。 這表示一旦從資料來源提取資料，與資料來源的實體連接就會中斷，但您仍然可以使用在**記錄集**物件本機快取的資料。  
  
 在開啟連接之後，將 SQL 字串指派給變數（sSQL）。 然後建立新**記錄集**物件的實例 `m_oRecordset1` 。 在下一行程式碼中，透過現有的**連接**開啟**記錄集**，並傳入 `sSQL` 做為**記錄集**的來源。 您可以協助 ADO 判斷做為**記錄集**來源而傳遞的 SQL 字串是命令的文字定義，其方式是將最後一個引數中的**AdCmdText**傳遞至**記錄集的 Open**方法。 這一行也會設定與**記錄集**相關聯的**LockType**和**CursorType** 。  
  
 下一行程式碼會將**MarshalOptions**屬性設定為等於**adMarshalModifiedOnly**。 **MarshalOptions**指出哪些記錄應該封送處理至仲介層（或 Web 服務器）。 如需封送處理的詳細資訊，請參閱 COM 檔。 當您使用**adMarshalModifiedOnly**搭配用戶端資料指標（[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)  =  **adUseClient**）時，只會將用戶端上已修改的記錄寫回中介層。 將**MarshalOptions**設定為**adMarshalModifiedOnly**可改善效能，因為封送處理的資料列較少。  
  
 接下來，將**記錄集**的**ActiveConnection**屬性設定為等於 [**無**]，將它中斷連接。 如需詳細資訊，請參閱[更新和保存資料](../../../ado/guide/data/updating-and-persisting-data.md)中的「中斷連接和重新連接記錄集」一節。  
  
 關閉資料來源的連接，並終結現有的**連接**物件。 這會釋出所耗用的資源。  
  
 最後一個步驟是將**記錄**集設定為表單上 Microsoft DataGrid 控制項的資料**源**，讓您可以輕鬆地在表單上顯示**記錄集**的資料。  
  
 按一下第二個按鈕 [**檢查資料**]。 這會執行**ExamineData**副程式。  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData 會使用**recordset**物件的各種方法和屬性，來顯示**記錄集中**資料的相關資訊。 它會使用**RecordCount**屬性來報告記錄的數目。 它會對**記錄集**執行迴圈，並在表單上的 [顯示] 文字方塊中列印**AbsolutePosition**屬性的值。 此外，在迴圈中，第三筆記錄的 [**書簽**] 屬性值會放入變數變數*vBookmark*中，以供稍後使用。  
  
 常式會使用稍早儲存的書簽變數，直接流覽回第三筆記錄。 常式會呼叫**WalkFields**副程式，這會迴圈處理**記錄集**的**Fields**集合，並顯示集合中每個**欄位**的詳細資料。  
  
 最後， **ExamineData**會將記錄**集**的**Filter**屬性僅用於具有等於2之 [**類別**] 的記錄。 套用此篩選準則的結果會立即顯示在表單的顯示格線中。  
  
 如需**ExamineData**副程式中所顯示功能的詳細資訊，請參閱[檢查資料](../../../ado/guide/data/examining-data.md)。  
  
 接下來，按一下第三個按鈕 [**編輯資料**]。 這會執行**EditData**副程式。  
  
## <a name="editdata"></a>EditData  
 當程式碼進入**EditData**副程式時，**記錄集**仍會在 [**類別**1] 上篩選為等於2，因此只會顯示符合篩選準則的專案。 它會先對**記錄集**執行迴圈，並將**記錄集**內每個可見專案的價格增加10%。 [**價格**] 欄位的值會藉由將該欄位的 [**值**] 屬性設定為等於新的有效數量來變更。  
  
 請記住，**記錄集**已與資料來源中斷連接。 在**EditData**中所做的變更只會對本機快取的資料複本進行。 如需詳細資訊，請參閱[編輯資料](../../../ado/guide/data/editing-data.md)。  
  
 除非您按一下第四個按鈕 [**更新資料**]，否則不會在資料來源上進行變更。 這會執行**UpdateData**副程式。  
  
## <a name="updatedata"></a>UpdateData  
 UpdateData 會先移除已套用至**記錄集**的篩選。 程式碼會移除並重設 `m_oRecordset1` 為表單上 Microsoft 系結 DataGrid 的**資料來源**，讓未篩選的**記錄集**出現在方格中。  
  
 然後，程式碼會使用**支援**方法搭配**adMovePrevious**引數，以查看您是否可以在**記錄集中**移動後置。  
  
 常式會使用**MoveFirst**方法移至第一筆記錄，並使用**Field**物件的**OriginalValue**和**Value**屬性，顯示欄位的原始和目前值。 [更新和保存資料](../../../ado/guide/data/updating-and-persisting-data.md)中會討論這些屬性，以及**UnderlyingValue**屬性（此處未使用）。  
  
 接下來，會建立新的**連接**物件，並用來重新建立資料來源的連接。 將**記錄集**重新連接至資料來源，方法是將新的**連接**設定為**記錄集**的**ActiveConnection** 。 為了將更新傳送至伺服器，程式碼會在**記錄集**上呼叫**UpdateBatch** 。  
  
 如果批次更新成功，模組層級的旗標變數 `m_flgPriceUpdated` 會設定為 True。 這會提醒您稍後清除對資料庫所做的所有變更。  
  
 最後，程式碼會移回**記錄集**內的第一筆記錄，並顯示原始和目前的值。 呼叫**UpdateBatch**之後，值會相同。  
  
 如需如何更新資料的詳細資訊，包括當您的**記錄集**中斷連接時，伺服器上的資料變更時該怎麼做，請參閱[更新和保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
## <a name="form_unload"></a>Form_Unload  
 **Form_Unload**副程式很重要，原因如下。 首先，因為這是一個範例應用程式，Form_Unload 清除在應用程式結束之前對資料庫所做的變更。 第二，程式碼會顯示如何使用**Execute**方法，直接從開啟的**連接**物件執行命令。 最後，它會顯示一個範例，說明如何針對資料來源執行不會傳回資料列的查詢（更新查詢）。
