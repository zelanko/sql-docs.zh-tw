---
title: "以程式設計方式管理封裝與資料夾 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: run-manage-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a40acf3a586c74119d948291fd179f78833cb37a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="managing-packages-and-folders-programmatically"></a>以程式設計方式管理封裝與資料夾
<a name="top"></a>當您以程式設計方式使用[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]封裝時，您可能想要判斷個別封裝或資料夾是否存在，或是管理儲存封裝所在的資料夾。 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空間的 <xref:Microsoft.SqlServer.Dts.Runtime> 類別，提供各種方法以滿足這些需求。    
    
##  <a name="exists"></a>判斷封裝或資料夾是否存在    
 若要以程式設計方式判斷儲存的封裝是否存在，請在嘗試載入和執行封裝之前，呼叫下列其中一個方法：    
    
|儲存位置|要呼叫的方法|    
|----------------------|--------------------|    
|SSIS 封裝存放區|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnSqlServer%2A>|    
    
 若要以程式設計方式判斷資料夾是否存在，請在嘗試列出資料夾中儲存的封裝之前，呼叫下列其中一個方法：    
    
|儲存位置|要呼叫的方法|    
|----------------------|--------------------|    
|SSIS 封裝存放區|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnSqlServer%2A>|    
    
 [回到頁首](#top)    
    
##  <a name="managing"></a>管理封裝與資料夾    
 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空間的 <xref:Microsoft.SqlServer.Dts.Runtime> 類別，提供管理封裝及儲存封裝之資料夾的其他方法。    
    
###  <a name="managing_rempkg"></a>移除封裝    
 若要以程式設計方式移除儲存的封裝，請呼叫下列其中一個方法：    
    
|儲存位置|要呼叫的方法|    
|----------------------|--------------------|    
|SSIS 封裝存放區|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|    
    
 [回到頁首](#top)    
    
###  <a name="managing_create"></a>建立資料夾    
 若要以程式設計方式建立儲存資料夾，請呼叫下列其中一個方法：    
    
|儲存位置|要呼叫的方法|    
|----------------------|--------------------|    
|SSIS 封裝存放區|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|    
    
 [回到頁首](#top)    
    
###  <a name="managing_remfldr"></a>移除資料夾    
 若要以程式設計方式移除儲存資料夾，請呼叫下列其中一個方法：    
    
|儲存位置|要呼叫的方法|    
|----------------------|--------------------|    
|SSIS 封裝存放區|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|    
    
 [回到頁首](#top)    
    
###  <a name="managing_rename"></a>重新命名資料夾    
 若要以程式設計方式重新命名儲存資料夾，請呼叫下列其中一個方法：    
    
|儲存位置|要呼叫的方法|    
|----------------------|--------------------|    
|SSIS 封裝存放區|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|    
    
 [回到頁首](#top)    
    
## <a name="see-also"></a>另請參閱    
 [封裝管理 &#40;SSIS 服務 &#41;](../../integration-services/service/package-management-ssis-service.md)     
 [以程式設計方式列舉可用的套件](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)    
    
  

