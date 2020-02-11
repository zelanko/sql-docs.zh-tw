---
title: 建立 CLR 觸發程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- CRL triggers
- DML triggers, CLR triggers
- DDL triggers, CLR triggers
ms.assetid: 31f41703-134d-49fc-9850-76c297351c2c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b68531b962b10785927c6212b2483f2d9c1d7d3a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62698823"
---
# <a name="create-clr-triggers"></a>建立 CLR 觸發程序
  您可以在內[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立資料庫物件，其在中是以 common language runtime [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] （CLR）所建立的元件進行程式設計。 可以使用 CLR 所提供之豐富程式設計模型的資料庫物件，包括 DML 觸發程序、DDL 觸發程序、預存程序、函數、彙總函式以及類型。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立 CLR 觸發程序 (DML 或 DDL) 包含下列步驟：  
  
-   以 .NET Framework 支援的語言，將觸發程序定義為類別。 如需如何在 CLR 中設計觸發程序的程式的詳細資訊，請參閱 [CLR 觸發程序](../../database-engine/dev-guide/clr-triggers.md)。 然後，使用適當的語言編譯器編譯類別，在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中建立組件。  
  
-   使用 CREATE ASSEMBLY 陳述式在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中登錄組件。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中之組件的詳細資訊，請參閱[組件 &#40;Database Engine&#41;](../clr-integration/assemblies-database-engine.md)。  
  
-   建立參考所登錄之組件的觸發程序。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中部署 SQL Server 專案，便會在已指定給專案的資料庫中註冊組件。 部署專案也會在資料庫中，為所有以 `SqlTrigger` 屬性註解的方法建立 CLR 觸發程序。 如需詳細資訊，請參閱 [Deploying CLR Database Objects](../clr-integration/deploying-clr-database-objects.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行 CLR 程式碼的功能預設為關閉。 您可以建立、改變和卸載參考 managed 程式碼模組的資料庫物件，但是除非使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [sp_configure （transact-sql）](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)來啟用[clr enabled 選項](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)，否則不會在中執行這些參考。  
  
 **若要建立、修改或卸除組件**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **若要建立 CLR 觸發程式**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)  
  
## <a name="see-also"></a>另請參閱  
 [DML 觸發程序](dml-triggers.md)   
 [Common Language Runtime &#40;CLR&#41; 整合程式設計概念](../clr-integration/common-language-runtime-clr-integration-programming-concepts.md)   
 [從 CLR 資料庫物件進行資料存取](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
