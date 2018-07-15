---
title: 伺服器組態-定序 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- collation configuration, SQL Server
- collation configuration, Setup
- collation configuration
ms.assetid: e3986870-5be4-458b-b671-5ff12a27b022
caps.latest.revision: 19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: abd57940e3caf8af66cb58fdeceebc802e877f6e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37290174"
---
# <a name="server-configuration---collation"></a>伺服器組態 - 定序
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈的 [伺服器組態 - 定序] 頁面上，您可以修改 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 用於排序的定序設定。 選取選項來比對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或另一部電腦之不同安裝的定序設定。  
  
## <a name="options"></a>選項。  
 針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 而自訂  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供兩組定序： Windows 定序和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]定序。 您可以對 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]指定個別的定序設定，也可以對這兩者指定相同的定序。  
  
 根據預設，系統會針對 US-English 系統地區設定選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序。 當地語系化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的預設定序是由電腦的 Windows 系統地區設定所決定。  
  
 只有當這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝的定序設定必須符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的另一個執行個體所使用的定序設定，或是定序設定必須符合另一部電腦的 Windows 系統地區設定時，您才應該變更預設設定。  
  
 **注意** [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 只會使用 Windows 定序。 如果您打算安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，請在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間選取 Windows 定序，以便確保 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]之間產生一致的結果。  
  
 如需詳細資訊，請參閱 [安裝程式中的定序設定](http://go.microsoft.com/fwlink/?LinkId=190977)。  
  
## <a name="best-practices"></a>最佳作法  
 如需 Windows 系統地區設定和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式所使用之對應預設定序的資料表的詳細資訊，請參閱 [安裝程式中的定序設定](http://go.microsoft.com/fwlink/?LinkId=190977)。  
  
 如果可能的話，請針對組織使用單一定序。 這樣您就不需要針對每個資料庫、資料行、運算式或識別碼明確指定定序。 如果您必須使用多重定序和字碼頁設定，則在編寫查詢程式碼時，必須考量定序優先順序的規則。 如需詳細資訊，請參閱[定序優先順序 &#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql) 的線上叢書主題。  
  
 當您選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的定序時，請考慮下列建議：  
  
-   如果可接受以二進位字碼指標為基礎的排序，請選取 BINARY2 定序。  
  
-   選取 Windows 定序以便跨資料類型進行一致的比較。  
  
-   為獲得更好的語言排序支援，請使用新的 100 層級定序。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
-   如果您計畫將資料庫移轉到升級的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體，請選取符合您現有資料庫定序的定序。  
  
  
