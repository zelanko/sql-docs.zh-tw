---
title: "IBCPSession (OLE DB) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-interfaces
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IBCPSession interface
ms.assetid: 00d0311f-8b71-4ad6-824d-0e89119347a3
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 650a7e2a10e6ebb45d8662e1cb33a3a42f7dfe1e
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **IBCPSession**介面會公開支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以檔案為基礎的大量複製作業。 **IBCPSession**介面會公開在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者在相同層級下的與工作階段。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者，資料來源物件是工作階段物件的 factory，且連接屬性 SSPROP_ENABLEBULKCOPY 中指定大量複製作業。 此外，SSPROP_ENABLEFASTLOAD 屬性應該要設定為 true。  
  
 呼叫**:: Createsession**方法接著會在建立**BulkCopySession**物件。 透過公開的所有檔案為基礎之大量複製方法**IBCPSession**物件接著會使用幾乎相同的簽章上可呼叫**IBCPSession**物件的**IBCPSession**介面。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援透過以記憶體為基礎的大量複製作業[IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)介面。  
  
 如需有關使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者大量複製作業，請參閱[執行大量複製作業](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)。  
  
 如需示範如何使用範例**IBCPSession**介面，請參閱[IBCPSession::BCPDone &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
|方法|Description|  
|------------|-----------------|  
|[IBCPSession::BCPColFmt &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)|在程式變數與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料行之間建立繫結。|  
|[IBCPSession::BCPColumns &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)|設定要繫結至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中之資料行的欄位數目。|  
|[IBCPSession::BCPControl &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)|設定大量複製作業的選項。|  
|[IBCPSession::BCPDone &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)|認可要傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的其餘資料列。|  
|[IBCPSession::BCPExec &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)|執行大量複製作業。|  
|[IBCPSession::BCPInit &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)|初始化大量複製結構、執行一些錯誤檢查、確認資料和格式檔案名稱正確無誤，然後開啟這些項目。|  
|[IBCPSession::BCPReadFmt &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)|從格式檔案中讀取每個資料行的格式資訊。|  
|[IBCPSession::BCPWriteFmt &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)|將每個資料行的格式資訊寫入格式檔案。|  
  
## <a name="see-also"></a>另請參閱  
 [介面 &#40; OLE DB &#41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
