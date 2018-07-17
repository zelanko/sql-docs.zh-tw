---
title: 建立使用者定義彙總 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: udf
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: c278b746-6323-4b32-b460-239915acc067
caps.latest.revision: 28
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a1f7c963f03fb295a79e8b21923cd43585d5291c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414327"
---
# <a name="create-user-defined-aggregates"></a>建立使用者定義彙總
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
  您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立資料庫物件，此功能是以 CLR 組件設計而成。 可以使用 CLR 提供之多種程式設計模型的資料庫物件，包括觸發程序、預存程序、函數、彙總函式和類型。  
  
 就像 [!INCLUDE[tsql](../../includes/tsql-md.md)]所提供的內建彙總函式一樣，使用者定義彙總函式會執行一組值的計算並傳回單一值。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立使用者定義彙總函式包含下列步驟：  
  
-   將使用者定義彙總函式定義為以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 支援的語言寫成的類別。 如需如何以 CLR 撰寫使用者定義彙總的詳細資訊，請參閱 [CLR 使用者定義彙總](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)。 使用適當的語言編譯器來編譯此類別以建立 CLR 組件。  
  
-   使用 CREATE ASSEMBLY 陳述式在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中登錄組件。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中之組件的詳細資訊，請參閱[組件 &#40;Database Engine&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)。  
  
-   使用 CREATE AGGREGATE 陳述式建立參考註冊組件的使用者自訂彙總。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中部署 SQL Server 專案，便會在已指定給專案的資料庫中註冊組件。 部署專案時，也會在資料庫中為所有以 **SqlUserDefinedAggregate** 屬性註解的類別定義建立使用者定義彙總。 如需詳細資訊，請參閱 [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行 CLR 程式碼的功能預設為關閉。 您可以建立、改變和卸除參考 Managed 程式碼模組的資料庫物件，但是除非使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_configure (Transact-SQL) [來啟用](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) [CLR 已啟用] 選項 [，否則在](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)中將無法執行這些參考。  
  
 **若要建立、修改或卸除組件**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **若要建立使用者自訂彙總**  
  
-   [CREATE AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [Common Language Runtime &#40;CLR&#41; 整合程式設計概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
