---
title: '步驟 5: DataControl 設為可用 （RDS 教學課程） |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], datacontrol made usable
ms.assetid: ed5c4a24-9804-4c85-817e-317652acb9b4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01b7a1b7829ace46cac7be21d33d9837845db9a7
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559735"
---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>步驟 5：將 DataControl 設為可用 (RDS 教學課程)
傳回**資料錄集**物件是可供使用。 您可以檢查、 瀏覽，或進行編輯，就像其他任何**資料錄集**。 您可以執行與**資料錄集**取決於您的環境。 Visual Basic 和 Visual c + + 有可用的視覺控制項**資料錄集**直接或間接與啟用的資料控制項的協助。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 例如，如果您要在 Microsoft Internet Explorer 中顯示網頁，您可能想要顯示**資料錄集**物件視覺控制項中的資料。 在網頁上的視覺控制項不能存取**資料錄集**直接物件。 不過，他們可以存取**Recordset**物件傳遞[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)。 **Rds。DataControl**根據視覺效果會成為可控制其[SourceRecordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)屬性設定為**資料錄集**物件。  
  
 視覺控制項物件必須具有其**DATASRC**參數設為**rds。DataControl**，並將其**DATAFLD**屬性設定為**資料錄集**物件欄位 （資料行）。  
  
 在本教學課程中，設定**SourceRecordset**屬性：  
  
```vb
Sub RDSTutorial5()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DC as New RDS.DataControl  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
   DC.SourceRecordset = RS         ' Visual controls can now bind to DC.  
...  
```  
  
## <a name="see-also"></a>另請參閱  
 [步驟 6： 變更傳送到伺服器 （RDS 教學課程）](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
