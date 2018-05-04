---
title: CreateObject 方法 (RDS) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5759c1b1b9faaaa9262879a614913a5fcf16c42
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="createobject-method-rds"></a>CreateObject 方法 (RDS)
建立目標商務物件的 proxy，並傳回的指標。 要與商務物件的通訊會透過網際網路傳送要求和資料的伺服器端 stub proxy 封裝和把資料。 同處理序元件物件，會使用任何 proxy，只是物件的指標會提供。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 遠端資料服務支援下列通訊協定： HTTP、 HTTPS (安全通訊端層透過 HTTP)、 DCOM 和同處理序。  
  
|通訊協定|語法|  
|--------------|------------|  
|HTTP|Set 物件 = DataSpace.CreateObject ("ProgId"，"http://awebsrvr")|  
|HTTPS|Set 物件 = DataSpace.CreateObject ("ProgId"，"https://awebsrvr")|  
|DCOM|Set object = DataSpace.CreateObject("ProgId", "computername")|  
|內含式|Set object = DataSpace.CreateObject("ProgId", "")|  
  
## <a name="parameters"></a>參數  
 *物件*  
 物件變數評估是在指定之類型的物件為*ProgID*。  
  
 *DataSpace*  
 物件變數，表示[.RDSDataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)用來建立新物件的執行個體的物件。  
  
 *ProgID*  
 A**字串**值，其中包含指定實作您的應用程式的商務規則的伺服器端的商務物件的程式設計識別項。  
  
 *awebsrvr*或*computername*  
 A**字串**值，表示用來識別伺服器商務物件的執行個體建立所在的網際網路資訊服務 (IIS) Web 伺服器的 URL。  
  
## <a name="remarks"></a>備註  
 *HTTP 通訊協定*是標準的 Web 通訊協定。*HTTPS*是安全的 Web 通訊協定。 使用*DCOM 通訊協定*執行時沒有 HTTP 的區域網路。 *同處理序*通訊協定是本機的動態連結程式庫 (DLL)，則不會使用網路。  
  
## <a name="applies-to"></a>適用於  
 [DataSpace 物件 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataFactory 物件、 查詢方法和 CreateObject 方法範例 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [資料空間物件和 CreateObject 方法範例 (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [CreateRecordset 方法 (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)


