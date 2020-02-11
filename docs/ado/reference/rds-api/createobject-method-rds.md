---
title: CreateObject 方法（RDS） |Microsoft Docs
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
ms.openlocfilehash: c6b50714cdff536418e759828d972c16abd7d7a0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964549"
---
# <a name="createobject-method-rds"></a>CreateObject 方法 (RDS)
建立目標商務物件的 proxy，並傳回它的指標。 Proxy 會封裝資料，並將其封送處理至伺服器端存根，以便與商務物件通訊，以透過網際網路傳送要求和資料。 對於同進程元件物件，不會使用任何 proxy，只會提供物件的指標。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 遠端資料服務支援下列通訊協定： HTTP、HTTPS （透過安全通訊端層的 HTTP）、DCOM 和同進程。  
  
|通訊協定|語法|  
|--------------|------------|  
|HTTP|Set object = CreateObject （"ProgId"，"HTTPs\://awebsrvr"）|  
|HTTPS|Set object = CreateObject （"ProgId"，"HTTPs\://awebsrvr"）|  
|DCOM|Set object = DataSpace.CreateObject("ProgId", "computername")|  
|內含式|Set object = DataSpace.CreateObject("ProgId", "")|  
  
## <a name="parameters"></a>參數  
 *Object*  
 評估為*ProgID*中所指定類型之物件的物件變數。  
  
 *空間*  
 代表 RDS 的物件變數[。](../../../ado/reference/rds-api/dataspace-object-rds.md)用來建立新物件實例的空間物件。  
  
 *進程*  
 **字串**值，其中包含指定用來執行應用程式之商務規則的伺服器端商務物件的程式設計識別碼。  
  
 *awebsrvr*或*computername*  
 **字串**值，表示用來識別建立伺服器商務物件實例之 INTERNET INFORMATION SERVICES （IIS）網頁伺服器的 URL。  
  
## <a name="remarks"></a>備註  
 *HTTP 通訊協定*是標準的 Web 通訊協定;*HTTPS*是安全的 Web 通訊協定。 在沒有 HTTP 的情況下執行區域網路時，請使用*DCOM 通訊協定*。 同*進程*通訊協定是本機動態程式庫（DLL）;它不會使用網路。  
  
## <a name="applies-to"></a>套用至  
 [DataSpace 物件 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataFactory 物件、Query 方法和 CreateObject 方法範例（VBScript）](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [空間物件和 CreateObject 方法範例（VBScript）](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [CreateRecordset 方法 (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)


