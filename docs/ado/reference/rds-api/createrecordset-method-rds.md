---
title: CreateRecordset 方法（RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl::CreateRecordset
- RDS.DataControl::CreateRecordset
- CreateRecordset
- RDSServer.DataFactory::CreateRecordset
- DataFactory::CreateRecordset
helpviewer_keywords:
- CreateRecordset method [RDS]
ms.assetid: 6840b1e5-c04d-4d3e-9dcc-42128c83492f
author: rothja
ms.author: jroth
ms.openlocfilehash: 53a391ccb25a32d628703543d95dc8e24668fcd5
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942490"
---
# <a name="createrecordset-method-rds"></a>CreateRecordset 方法 (RDS)
建立空的、中斷連接的[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.CreateRecordset(ColumnInfos)  
```  
  
#### <a name="parameters"></a>參數  
 *Object*  
 代表[RDSServer DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)或 RDS 的物件變數[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 *ColumnsInfos*  
 屬性的**Variant**陣列，定義所建立之**記錄集中**的每個資料行。 每個資料行定義都包含四個必要屬性的陣列和一個選擇性的屬性。  
  
|屬性|描述|  
|---------------|-----------------|  
|名稱|欄標題的名稱。|  
|類型|資料類型的整數。|  
|Size|寬度（以字元為單位）的整數，不論資料類型為何。|  
|Null 屬性|布林值。|  
|Scale （選擇性）|這個選擇性屬性會定義數值欄位的尺規。 如果未指定此值，數值會被截斷為三個小數位數。 精確度不受影響，但小數點後面的位數將會截斷為三。|  
  
 然後，資料行陣列集會組成陣列，以定義**記錄集**。  
  
## <a name="remarks"></a>備註  
 伺服器端商務物件可以將來自非 OLE DB 資料提供者的資料（例如包含股票報價的作業系統檔案）填入產生的**記錄集**。  
  
 下表列出**CreateRecordset**方法所支援的[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值。 列出的數位是用來定義欄位的參考編號。  
  
 每個資料類型都是固定長度或可變長度。 固定長度的類型應定義為-1，因為已預先決定大小，而且仍然需要大小定義。 可變長度的資料類型允許從1到32767的大小。  
  
 針對某些變數資料類型，類型可以強制轉型為替代欄位中所記下的類型。 在建立並填入**記錄集**之前，您將不會看到替換。 然後，您可以視需要檢查實際的資料類型。  
  
|長度|持續性|Number|Substitution|  
|------------|--------------|------------|------------------|  
|已修正|**adTinyInt**|16||  
|已修正|**adSmallInt**|2||  
|已修正|**adInteger**|3||  
|已修正|**adBigInt**|20||  
|已修正|**adUnsignedTinyInt**|17||  
|已修正|**adUnsignedSmallInt**|18||  
|已修正|**adUnsignedInt**|19||  
|已修正|**adUnsignedBigInt**|21||  
|已修正|**adSingle**|4||  
|已修正|**adDouble**|5||  
|已修正|**adCurrency**|6||  
|已修正|**adDecimal**|14||  
|已修正|**adNumeric**|131||  
|已修正|**adBoolean**|11||  
|已修正|**adError**|10||  
|已修正|**adGuid**|72||  
|已修正|**adDate**|7||  
|已修正|**adDBDate**|133||  
|已修正|**adDBTime**|134||  
|已修正|**adDBTimestamp**|135|7|  
|變數|**adBSTR**|8|130|  
|變數|**adChar**|129|200|  
|變數|**adVarChar**|200||  
|變數|**adLongVarChar**|201|200|  
|變數|**adWChar**|130||  
|變數|**adVarWChar**|202|130|  
|變數|**adLongVarWChar**|203|130|  
|變數|**adBinary**|128||  
|變數|**adVarBinary**|204||  
|變數|**adLongVarBinary**|205|204|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [CreateRecordset 方法範例（VB）](../../../ado/reference/ado-api/createrecordset-method-example-vb.md)   
 [CreateRecordset 方法範例（VBScript）](../../../ado/reference/rds-api/createrecordset-method-example-vbscript.md)   
 [CreateObject 方法 (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)



