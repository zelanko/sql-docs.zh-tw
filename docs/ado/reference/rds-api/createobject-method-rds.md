---
title: CreateObject 方法 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d220a9abc0e2dc72d7ab65306b514a9925b4fc43
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281063"
---
# <a name="createobject-method-rds"></a>CreateObject 方法 (RDS)
建立目標商務物件的 proxy，並傳回的指標。 要透過網際網路傳送要求和資料與商務物件通訊的伺服器端 stub proxy 封裝和封送處理資料。 同處理序元件物件會使用任何 proxy，只是物件的指標會提供。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 遠端資料服務支援下列通訊協定：HTTP、 HTTPS (HTTP 透過安全通訊端層)、 DCOM 和同處理序。  
  
|Protocol|語法|  
|--------------|------------|  
|HTTP|Set object = DataSpace.CreateObject("ProgId", "https\://awebsrvr")|  
|HTTPS|Set object = DataSpace.CreateObject("ProgId", "https\://awebsrvr")|  
|DCOM|Set object = DataSpace.CreateObject("ProgId", "computername")|  
|內含式|Set object = DataSpace.CreateObject("ProgId", "")|  
  
## <a name="parameters"></a>參數  
 *物件*  
 物件變數評估為在指定之類型的物件*ProgID*。  
  
 *DataSpace*  
 物件變數，表示[rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)用來建立新物件的執行個體的物件。  
  
 *ProgID*  
 A**字串**值，其中包含指定的伺服器端商務物件，實作您的應用程式的商務規則的程式設計識別項。  
  
 *awebsrvr*或*computername*  
 A**字串**值，表示用來識別伺服器商務物件的執行個體建立的 Internet Information Services (IIS) Web 伺服器的 URL。  
  
## <a name="remarks"></a>備註  
 *HTTP 通訊協定*是標準的 Web 通訊協定;*HTTPS*是安全的 Web 通訊協定。 使用*DCOM 通訊協定*執行時沒有 HTTP 的區域網路。 *同處理序*通訊協定是本機的動態連結程式庫 (DLL)，它不會使用網路。  
  
## <a name="applies-to"></a>適用於  
 [DataSpace 物件 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataFactory 物件、 查詢方法和 CreateObject 方法範例 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [DataSpace 物件和 CreateObject 方法範例 (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [CreateRecordset 方法 (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)


