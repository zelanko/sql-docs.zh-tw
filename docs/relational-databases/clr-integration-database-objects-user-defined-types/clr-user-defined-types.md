---
title: CLR 使用者定義類型 |微軟文件
description: 本文介紹了創建使用者定義類型 (UDT) 以在 SQL Server 資料庫中存儲 CLR 物件的過程。
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- validation [CLR integration]
- types [CLR integration]
- UserDefined serialization format [CLR integration]
- null values [CLR integration]
- serialization
- Native serialization format [CLR integration]
- databases [CLR integration]
- building database objects [CLR integration], user-defined types
- user-defined types [CLR integration]
- common language runtime [SQL Server], user-defined types
- UDTs [CLR integration]
- database objects [CLR integration], user-defined types
- turning on CLR functionality
- customizing UDT expression return types [CLR integration]
- UDTs [CLR integration], about UDTs
- comparing UDT values
- annotations [CLR integration]
- user-defined types [CLR integration], about UDTs
- variables [CLR integration]
- invoking UDT methods
- indexes [CLR integration]
ms.assetid: 27c4889b-c543-47a8-a630-ad06804f92df
author: rothja
ms.author: jroth
ms.openlocfilehash: b3983459ac8ca4b38c82cc926c2f1b0f55bb1d58
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487857"
---
# <a name="clr-user-defined-types"></a>CLR 使用者定義型別
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使您能夠創建根據 .NET Framework 通用語言運行時 (CLR) 中建立的程式集程式設計的資料庫物件。 資料庫物件可充分運用 CLR 所提供的豐富程式設計模型，包括觸發程序、預存程序、函數、彙總函式和類型等。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，執行 CLR 程式碼的功能預設會設定為 OFF。 可以使用**sp_configure**系統儲存過程啟用CLR。  
  
 從[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]開始,可以使用使用者定義的類型 (UDT) 來擴展伺服器的標量類型系統,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]從而在資料庫中存儲 CLR 物件。 UDT 可以包含多個元素並可以具有行為，使其有別於由單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型組成的傳統別名資料類型。  
  
 因為系統將 UDT 當做一個整體來進行存取，所以它們使用的複雜資料類型可能會對效能產生負面影響。 通常使用傳統資料列及資料表可以對複雜資料進行最佳模型化。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 UDT 適用於以下項目：  
  
-   日期、時間、貨幣及擴充的數值類型  
  
-   Geospatial 應用程式  
  
-   編碼或加密的資料  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中開發 UDT 的過程包含下列步驟：  
  
1.  **編寫和建立定義 UDT 的組件。** UDT 是使用會產生可驗證程式碼之 .NET Framework Common Language Runtime (CLR) 支援的任何語言所定義。 這包括 Visual C# 和 Visual Basic .NET。 資料會公開為 .NET Framework 類別或結構的欄位及屬性，並且其行為是由類別或結構的方法所定義。  
  
2.  **註冊組件。** UDT 可透過資料庫專案中的 Visual Studio 使用者介面進行部署[!INCLUDE[tsql](../../includes/tsql-md.md)],或者透過使用 CREATE ASSEMBLY 語句進行部署,該語句將包含類或結構的程式集複製到資料庫中。  
  
3.  **在 SQL Server 中建立 UDT。** 將程式集載入到主機資料庫中後,可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)]CREATE TYPE 語句創建 UDT,並將類或結構的成員公開為 UDT 的成員。 UDT 僅存在於單一資料庫的內容中，並且一旦註冊後，就不再與建立它們的外部檔案具有相依性。  
  
    > [!NOTE]  
    >  在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 之前，不支援從 .NET Framework 組件建立的 UDT。 但是,您仍[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以使用別名資料類型,使用**sp_addtype**。 CREATE TYPE 語法可用來建立原生 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者定義資料類型及 UDT。  
  
4.  **使用 UDT 建立表、變數或參數**從[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]開始,使用者定義的類型可用作表的列定義、[!INCLUDE[tsql](../../includes/tsql-md.md)]批次處理中的變數或[!INCLUDE[tsql](../../includes/tsql-md.md)]函數或儲存過程的參數。  
  
## <a name="in-this-section"></a>本節內容  
 [建立使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
 描述如何建立 UDT。  
  
 [在 SQL Server 中註冊使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/registering-user-defined-types-in-sql-server.md)  
 描述如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中註冊及管理 UDT。  
  
 [使用 SQL Server 中的使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)  
 描述如何使用 UDT 建立查詢。  
  
 [存取 ADO.NET 中的使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-in-ado-net.md)  
 描述如何在 ADO.NET 中，使用 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來處理 UDT。  
  
  
