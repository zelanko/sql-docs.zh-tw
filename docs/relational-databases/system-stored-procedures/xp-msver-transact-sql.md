---
title: xp_msver & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_msver_TSQL
- xp_msver
dev_langs:
- TSQL
helpviewer_keywords:
- xp_msver
ms.assetid: 9264cf8c-92ba-45ad-b2d6-15d26d805a16
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b936f00f449bd57a7a00fa825910a809a1baf225
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898369"
---
# <a name="xpmsver-transact-sql"></a>xp_msver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回有關的版本資訊[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 **xp_msver**也會傳回伺服器的實際組建編號的相關資訊以及有關伺服器環境的資訊。 資訊的**xp_msver**傳回可用於[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式、 批次、 預存程序，並依此類推，以加強平台獨立程式碼邏輯。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_msver [ optname ]  
```  
  
## <a name="arguments"></a>引數  
 *optname*  
 這是選項的名稱，它可以是下列值之一。  
  
|選項/資料行名稱|描述|  
|-------------------------|-----------------|  
|**ProductName**|產品名稱;例如， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**ProductVersion**|產品版本。|  
|**語言**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的語言版本。|  
|**平台**|執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之電腦的作業系統名稱、製造商名稱和晶片家族名稱。|  
|**註解**|有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的其他資訊。|  
|**公司名稱**|產生 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的公司名稱；例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corporation。|  
|**FileDescription**|作業系統。|  
|**FileVersion**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可執行檔的版本。|  
|**InternalName**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部名稱；例如 SQLSERVR。|  
|**LegalCopyright**|必要的合法著作權資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; 例如 Copyright © [!INCLUDE[msCoName](../../includes/msconame-md.md)] corp.1988-2005.|  
|**LegalTrademarks**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必要的合法商標資訊。 例如，[!INCLUDE[msCoName](../../includes/msconame-md.md)] 是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corporation 的註冊商標。|  
|**OriginalFilename**|在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動時執行的檔案名稱；例如 Sqlservr.exe。|  
|**PrivateBuild**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**SpecialBuild**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**WindowsVersion**|執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 之電腦所安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 版本。|  
|**ProcessorCount**|執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之電腦的處理器數目。|  
|**ProcessorActiveMask**|指出執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦中已安裝的處理器，由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 啟動及使用。|  
|**ProcessorType**|處理器類型。 類似於**平台**。|  
|**PhysicalMemory**|執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之電腦所安裝的 RAM 數量 (以 MB 為單位)。|  
|**產品識別碼**|產品識別碼 (PID)。 這是在安裝期間指定的。 這個號碼位於原廠 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 光碟片外盒的貼紙上。|  
  
## <a name="return-code-values"></a>傳回碼值  
 1 （成功）  
  
## <a name="result-sets"></a>結果集  
 **xp_msver**，不含任何參數，會傳回四資料行結果集，其中列出所有選項值。 **xp_msver**，針對任何參數，會傳回四資料行結果集使用該選項的值。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [一般擴充預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [@@VERSION &#40;Transact-SQL&#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)  
  
  
