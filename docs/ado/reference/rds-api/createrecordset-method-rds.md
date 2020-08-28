---
description: CreateRecordset 方法 (RDS)
title: " (RDS) 的 CreateRecordset 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: a459ddea3716bb918ed18a49d632e20a9e4557fd
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982519"
---
# <a name="createrecordset-method-rds"></a>CreateRecordset 方法 (RDS)
建立空白、中斷連接的 [記錄集](../ado-api/recordset-object-ado.md)。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.CreateRecordset(ColumnInfos)  
```  
  
#### <a name="parameters"></a>參數  
 *Object*  
 代表 [RDSServer. DataFactory](./datafactory-object-rdsserver.md) 或 RDS 的物件變數。 [DataControl](./datacontrol-object-rds.md) 物件。  
  
 *ColumnsInfos*  
 屬性的 **Variant** 陣列，定義建立的 **記錄集** 內的每個資料行。 每個資料行定義都包含四個必要屬性的陣列和一個選擇性屬性。  
  
|屬性|描述|  
|---------------|-----------------|  
|名稱|欄標題的名稱。|  
|類型|資料類型的整數。|  
|大小|寬度的整數（以字元為單位），不論資料類型為何。|  
|Null 屬性|布林值。|  
|調整 (選用) |這個選擇性屬性會定義數值欄位的小數位數。 如果未指定此值，則會將數值截斷為三個小數位數。 精確度不受影響，但小數點之後的位數將會截斷為三。|  
  
 然後，會將資料行陣列集分組到定義 **記錄集**的陣列中。  
  
## <a name="remarks"></a>備註  
 伺服器端商務物件可以將來自非 OLE DB 資料提供者的資料填入產生的 **記錄集** ，例如包含股票報價的作業系統檔案。  
  
 下表列出**CreateRecordset**方法所支援的[DataTypeEnum](../ado-api/datatypeenum.md)值。 列出的數位是用來定義欄位的參考編號。  
  
 每個資料類型都可能是固定長度或可變長度。 固定長度類型的定義大小應為-1，因為大小是預先決定的，且仍然需要大小定義。 可變長度的資料類型允許從1到32767的大小。  
  
 針對部分變數資料類型，類型可以強制轉型為替代資料行中所注明的型別。 在建立並填入 **記錄集** 之前，您將不會看到這些替代。 然後，您可以視需要檢查實際的資料類型。  
  
|長度|持續性|Number|Substitution|  
|------------|--------------|------------|------------------|  
|固定式|**adTinyInt**|16||  
|固定式|**adSmallInt**|2||  
|固定式|**adInteger**|3||  
|固定式|**adBigInt**|20||  
|固定式|**adUnsignedTinyInt**|17||  
|固定式|**adUnsignedSmallInt**|18||  
|固定式|**adUnsignedInt**|19||  
|固定式|**adUnsignedBigInt**|21||  
|固定式|**adSingle**|4||  
|固定式|**adDouble**|5||  
|固定式|**adCurrency**|6||  
|固定式|**adDecimal**|14||  
|固定式|**adNumeric**|131||  
|固定式|**adBoolean**|11||  
|固定式|**adError**|10||  
|固定式|**adGuid**|72||  
|固定式|**adDate**|7||  
|固定式|**adDBDate**|133||  
|固定式|**adDBTime**|134||  
|固定式|**adDBTimestamp**|135|7|  
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
        [DataControl 物件 (RDS)](./datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [DataFactory 物件 (RDSServer)](./datafactory-object-rdsserver.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [ (VB) 的 CreateRecordset 方法範例 ](../ado-api/createrecordset-method-example-vb.md)   
 [ (VBScript) 的 CreateRecordset 方法範例 ](./createrecordset-method-example-vbscript.md)   
 [CreateObject 方法 (RDS)](./createobject-method-rds.md)