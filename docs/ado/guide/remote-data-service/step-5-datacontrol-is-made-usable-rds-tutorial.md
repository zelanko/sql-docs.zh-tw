---
title: "步驟 5: DataControl 已進行使用 （RDS 教學課程） |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: RDS tutorial [ADO], datacontrol made usable
ms.assetid: ed5c4a24-9804-4c85-817e-317652acb9b4
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 45e7605b16c224e4b299c0f1454dec9372ccd929
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>步驟 5: DataControl 已進行使用 （RDS 教學課程）
傳回**資料錄集**物件是可供使用。 您可以檢查、 瀏覽，或進行編輯，就像其他任何**資料錄集**。 您可以使用達成**資料錄集**取決於您的環境。 Visual Basic 和 Visual c + + 已經可以使用的視覺控制項**資料錄集**直接或間接與啟用的資料控制項的協助。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 例如，如果您要在 Microsoft Internet Explorer 中顯示網頁，可能會想要顯示**資料錄集**物件視覺控制項中的資料。 在網頁上的視覺控制項不能存取**資料錄集**直接物件。 不過，他們可以存取**資料錄集**物件透過[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)。 **.RDSDataControl**的視覺效果會變成可用時控制其[SourceRecordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)屬性設定為**資料錄集**物件。  
  
 視覺控制項物件必須具有其**DATASRC**參數設定為**.RDSDataControl**，且其**DATAFLD**屬性設定為**資料錄集**物件欄位 （資料行）。  
  
 在本教學課程中，設定**SourceRecordset**屬性：  
  
```  
Sub RDSTutorial5()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DC as New RDS.DataControl  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
   DC.SourceRecordset = RS         ' Visual controls can now bind to DC.  
...  
```  
  
## <a name="see-also"></a>請參閱  
 [步驟 6： 變更傳送到伺服器 （RDS 教學課程）](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
