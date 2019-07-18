---
title: 匯出和匯入資料採礦物件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [Analysis Services]
- exporting mining models
- exporting mining structures
- mining structures [Analysis Services], creating
- mining structures [DMX], exporting
- mining models [Analysis Services], migration
ms.assetid: 10a83b13-2640-4ff5-80c8-a35e1d692908
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c2f79f8bf9a1d0ff01ba97d29662fab026d4adcd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084464"
---
# <a name="export-and-import-data-mining-objects"></a>匯出及匯入資料採礦物件
  除了在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中針對備份、還原和移轉方案提供的功能之外，SQL Server 資料採礦還可以使用資料採礦延伸模組 (DMX)，在不同的伺服器之間快速傳送資料採礦結構和模型。  
  
 如果您的資料採礦方案使用關聯式資料，而非多維度資料庫，則使用 `EXPORT` 和 `IMPORT` 傳送模型要比使用資料庫還原或部署整個方案更為快速而且容易。  
  
 本節提供如何使用 DMX 陳述式傳送資料採礦結構與模型的概觀。 如需語法及範例的詳細資訊，請參閱 [EXPORT &#40;DMX&#41;](/sql/dmx/export-dmx) 和 [IMPORT &#40;DMX&#41;](/sql/dmx/import-dmx)。  
  
> [!NOTE]  
>  您必須是資料庫或伺服器管理員，才能從 Microsoft SQL Server Analysis Services 資料庫匯出或匯入物件。  
  
## <a name="exporting-data-mining-structures"></a>匯出資料採礦結構  
 當您匯出採礦結構時，EXPORT 陳述式會自動匯出所有關聯的模型。 如果您要控制匯出的物件，必須依名稱指定每個物件。  
  
 當您匯出採礦結構時，如果採礦結構已經過處理，而且結果已經經過快取 (這是預設行為)，定義則包含結構所依據之資料的摘要。 若要移除此摘要，您必須執行 `Process Clear Structure` 作業，清除與採礦結構關聯的快取。 如需詳細資訊，請參閱 [處理採礦結構](process-a-mining-structure.md)。  
  
### <a name="exporting-data-mining-models"></a>匯出資料採礦模型  
 您可以使用 `WITH DEPENDENCIES` 關鍵字匯出資料來源與資料來源檢視定義，以及採礦模型及其結構。  
  
 當您匯出採礦模型而不匯出其相依性時，EXPORT 陳述式會匯出採礦模型及其採礦結構的定義，但是不會匯出資料來源的定義。 因此，在您匯入模型後，您將能夠立即瀏覽模型，但是，如果您要在目標伺服器上重新處理採礦模型，或針對基礎資料執行查詢，則必須在目的地伺服器上建立對應的資料來源。  
  
## <a name="importing-data-mining-structures-and-models"></a>匯入資料採礦結構和模型  
 當您匯入資料採礦物件時，該物件會匯入您執行 IMPORT 陳述式時所連接的伺服器和資料庫。 如果匯入檔案包含的資料庫不存在於伺服器上，則會建立資料庫。  
  
 您也可以使用 `Restore` 命令匯入採礦結構或採礦模型。 您的模型或結構將會還原到與匯出之來源資料庫同名的資料庫中。 如需詳細資訊，請參閱 [Restore Options](../multidimensional-models/restore-options.md)。  
  
## <a name="remarks"></a>備註  
 如果伺服器上已存在相同名稱的模型或結構，則無法將該模型或結構匯入到該伺服器中。 同時，您無法匯入資料採礦物件，然後在匯出檔案中修改該物件的名稱。 因此，如果您預期會發生命名衝突，應該刪除目標伺服器上的資料採礦物件，或在匯出定義前，先重新命名該資料採礦物件。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦方案與物件的管理](management-of-data-mining-solutions-and-objects.md)  
  
  
