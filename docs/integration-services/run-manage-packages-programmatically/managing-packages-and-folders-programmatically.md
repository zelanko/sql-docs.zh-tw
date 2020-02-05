---
title: 以程式設計方式管理套件與資料夾 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a14ae64026443324f7a5dc3f47dcea15f9907f5f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71295725"
---
# <a name="managing-packages-and-folders-programmatically"></a>以程式設計方式管理封裝與資料夾

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


<a name="top"></a> 當您以程式設計方式使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件時，您可能想要判斷個別的套件或資料夾是否存在，或是管理儲存套件的資料夾。 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空間的 <xref:Microsoft.SqlServer.Dts.Runtime> 類別，提供各種方法以滿足這些需求。    
    
##  <a name="exists"></a> 判斷套件或資料夾是否存在    
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
    
##  <a name="managing"></a> 管理套件與資料夾    
 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空間的 <xref:Microsoft.SqlServer.Dts.Runtime> 類別，提供管理封裝及儲存封裝之資料夾的其他方法。    
    
###  <a name="managing_rempkg"></a> 移除套件    
 若要以程式設計方式移除儲存的封裝，請呼叫下列其中一個方法：    
    
|儲存位置|要呼叫的方法|    
|----------------------|--------------------|    
|SSIS 封裝存放區|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|    
    
 [回到頁首](#top)    
    
###  <a name="managing_create"></a> 建立資料夾    
 若要以程式設計方式建立儲存資料夾，請呼叫下列其中一個方法：    
    
|儲存位置|要呼叫的方法|    
|----------------------|--------------------|    
|SSIS 封裝存放區|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|    
    
 [回到頁首](#top)    
    
###  <a name="managing_remfldr"></a> 移除資料夾    
 若要以程式設計方式移除儲存資料夾，請呼叫下列其中一個方法：    
    
|儲存位置|要呼叫的方法|    
|----------------------|--------------------|    
|SSIS 封裝存放區|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|    
    
 [回到頁首](#top)    
    
###  <a name="managing_rename"></a> 重新命名資料夾    
 若要以程式設計方式重新命名儲存資料夾，請呼叫下列其中一個方法：    
    
|儲存位置|要呼叫的方法|    
|----------------------|--------------------|    
|SSIS 封裝存放區|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|    
    
 [回到頁首](#top)    
    
## <a name="see-also"></a>另請參閱    
 [套件管理 &#40;SSIS 服務&#41;](../../integration-services/service/package-management-ssis-service.md)     
 [以程式設計方式列舉可用的套件](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)    
    
  
