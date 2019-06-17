---
title: CLR 整合安全性中的連結 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- table-access links [CLR integration]
- security [CLR integration]
- invocation links [CLR integration]
- gated links [CLR integration]
ms.assetid: 168efd01-d12e-4bdf-a1b3-0b5c76474eaf
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 37aa64129658128bd7297f147f317166917e05a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62781067"
---
# <a name="links-in-clr-integration-security"></a>CLR 整合安全性中的連結
  本節將描述使用者程式碼片段如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或其中一種 Managed 語言在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中彼此呼叫。 這些物件之間的關聯性稱為連結。  
  
## <a name="invocation-links"></a>引動過程連結  
 引動過程連結會對應至來自呼叫物件之使用者 (例如呼叫預存程序的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次) 或是 Common Language Runtime (CLR) 預存程序或函數的程式碼引動過程。 引動過程連結會導致系統檢查被呼叫者的 `EXECUTE` 權限。  
  
## <a name="table-access-links"></a>資料表存取連結  
 資料表存取連結會對應至擷取或修改資料表、檢視表或資料表值函式中的值。 它們與引動過程連結類似，但它們在 SELECT、INSERT、UPDATE 及 DELETE 權限方面具有更精細的存取控制。  
  
## <a name="gated-links"></a>閘門守護式連結  
 閘門守護式連結表示在執行期間，一旦建立了物件關聯性，就不會檢查該物件關聯性兩端的權限。 兩個物件之間的閘門守護式的連結時 (例如，物件**x**和物件**y**)，物件的權限**y**和其他物件從物件存取**y**只檢查物件的建立時間**x**。 在物件的建立時間**x**，`REFERENCE`上檢查權限**y**的擁有者對**x**。 在執行階段 (例如，當某人呼叫物件**x**)，根據檢查沒有權限**y**或它以靜態方式參考其他物件。 在執行時，將適當的權限檢查對物件**x**本身。  
  
 閘門守護式連結一定會搭配兩個物件之間的中繼資料相依性使用。 這個中繼資料相依性就是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目錄中建立的關聯性，只要其他相依的物件存在，就可防止物件被卸除。  
  
 當不適合進行或無法管理提供權限給許多相依物件的作業時，閘門守護式連結就很有用。 閘門守護式連結會導入物件之間，以便定義 CLR 組件 (例如，CLR 程序、觸發程序、函數、類型和彙總) 與定義這些組件之來源組件的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 進入點。 針對這些物件進行的閘門守護式安全性表示，若要叫用 CLR 組件中定義的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 進入點，呼叫者只需要該 [!INCLUDE[tsql](../../includes/tsql-md.md)] 進入點的適當權限。 呼叫者不需要擁有該組件或它以靜態方式參考之任何其他組件的權限。 系統會在建立 [!INCLUDE[tsql](../../includes/tsql-md.md)] 進入點時檢查組件的權限。  
  
## <a name="sql-server-authorization-based-security"></a>以 SQL Server 授權為基礎的安全性  
 下面是以 CLR 為基礎之資料庫物件本身和之間之引動過程的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性檢查基本規則：前三項規則會定義要針對哪個物件檢查哪些權限，而第四項規則會定義要針對哪個執行內容檢查權限。  
  
1.  除非引動過程在相同的物件內部進行，否則所有引動過程都需要 `EXECUTE` 權限。這表示相同組件內部的呼叫不需要進行任何權限檢查。 在執行時檢查權限。  
  
2.  建立呼叫物件時，閘門守護式連結需要被呼叫者的 `REFERENCE` 權限。 當建立物件時，系統會檢查呼叫物件之擁有者的權限。  
  
3.  針對要存取的資料表或檢視表，資料表存取連結需要對應的 `SELECT`、`INSERT`、`UPDATE` 或 `DELETE` 權限。  
  
4.  針對目前的執行內容，檢查權限。 您可以使用與呼叫者不同的執行內容來建立程序和函數。 不過，組件一定會使用針對它定義之程序、函數或觸發程序的執行內容建立。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合安全性](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
