---
title: 建立新原則或開啟原則對話方塊，一般頁面 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.policy.f1
- sql13.swb.dmf.policy.filter.f1
- sql13.swb.dmf.newgroup.f1
ms.assetid: c00bebd0-d04b-4c64-840e-8b7a2c603436
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ae5b12473756d6ca5c5a20b188b3c282205d9bd9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137896"
---
# <a name="create-new-policy-or-open-policy-dialog-box-general-page"></a>建立新原則或開啟原則對話方塊，一般頁面
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用此對話方塊可建立新的以原則為基礎的管理原則，或是修改現有的原則。 使用 **[針對目標]** 和 **[伺服器限制]** 區域當做篩選，將原則限制為所有可能目標的子集。 如果是要當做目標篩選使用的條件，必須在實體 Facet 上定義這些條件，而且這些條件不能包含函數和 LIKE 運算子。 當系統計算原則的物件集時，根據預設會排除系統物件。  例如，如果原則的物件集是指所有資料表，則原則不會套用至系統資料表。 如果使用者想要對系統物件評估原則，可以明確地將系統物件加入至物件集。 不過，雖然 **check on schedule** 評估模式支援所有原則，但基於效能的考量， **check on change** 評估模式並未支援所有原則與任意物件集搭配使用。 如需詳細資訊，請參閱 [https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx](https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx)  
  
## <a name="options"></a>選項。  
 **名稱**  
 如果是新的原則，請輸入新原則的名稱。 如果是現有的原則，則會顯示名稱。  
  
 **已啟用**  
 選取 [已啟用]  核取方塊可啟用此原則。 清除 **[已啟用]** 核取方塊可停用此原則。 **[已啟用]** 方塊適用於原則 Automation， 它會建立或移除原則的 Automation 系統。 Automation 使用下列機制：  
  
 **變更時 - 避免**  
 資料庫觸發程序會強制執行相容性。  
  
 **變更時 - 僅限記錄**  
 通知服務事件會檢查相容性。  
  
 **按排程時間**  
 建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業來按排程時間檢查相容性。  
  
 使用 **[視需要]** 評估模式執行的原則不會使用這個核取方塊。  
  
 **檢查條件**  
 選取這個原則使用之以原則為基礎的管理條件。 伺服器上關聯之以原則為基礎之管理 Facet 的條件都會列出來。 按一下 **[新增條件]** 即可建立新條件。 按一下省略符號 ( **...** ) 按鈕即可修改條件。  
  
 **[針對目標]**  
 選取可供這個 Facet 使用的目標類型，以完成篩選運算式。  
  
 **評估模式**  
 選取此原則的評估模式。 某些原則可加以檢查，但不會強制執行。 評估模式如下所示：  
  
 **[視需要]**  
 只有當您從 [評估]  對話方塊執行原則時，才可以執行。  
  
 **按排程時間**  
 定期評估原則、針對具有不相容的原則記下記錄項目，並建立報表。 啟用 **[排程]** 方塊。  
  
 **變更時 - 僅限記錄**  
 當嘗試變更時，這個選項不會阻止不相容的變更，但是會記錄原則違規。  
  
 **變更時 - 避免**  
 當嘗試變更時，這個選項會阻止將違反原則的變更。  
  
 **[排程]**  
 當選取 [按排程時間]  評估模式時會出現這個選項。 輸入排程的名稱、按一下 **[挑選]** 從清單中選取排程，或是按一下 **[新增]** 建立新的排程。 若要啟用排程區域，必須選取 **[按排程時間]** 。  
  
 **[伺服器限制]**  
 選取適合此原則的伺服器類型。 選項為 **[無]** 或是選取用來篩選可能之伺服器的條件。  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來管理伺服器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
