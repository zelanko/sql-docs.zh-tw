---
title: Refresh 方法 (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords:
- Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 822430c56070bb459e36ca3a3310d186258aea34
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298224"
---
# <a name="refresh-method-rds"></a>Refresh 方法 (RDS)
重新查詢中指定的資料來源[Connect](../../../ado/reference/rds-api/connect-property-rds.md)屬性和更新查詢結果。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 物件變數，表示[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
## <a name="remarks"></a>備註  
 您必須設定[Connect](../../../ado/reference/rds-api/connect-property-rds.md)，[伺服器](../../../ado/reference/rds-api/server-property-rds.md)，並[SQL](../../../ado/reference/rds-api/sql-property.md)屬性，才能使用**重新整理**方法。 與相關聯的表單上的所有資料繫結控制項**rds。DataControl**物件將會反映新的記錄集。 已存在的任何[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)釋放物件，並捨棄任何未儲存的變更。 **重新整理**方法便會自動將第一筆記錄目前的記錄。  
  
 它是個不錯的主意，呼叫**重新整理**方法定期當您使用的資料。 如果您擷取資料，然後將它的用戶端電腦上，保留一段時間，就可能會變成過期。 可以，任何您所做的變更將會失敗，因為其他人可能已變更記錄，並送出變更之前。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [Refresh 方法範例 (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Refresh 方法範例 (VBScript)](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [通訊錄命令按鈕](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate 方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


