---
title: "使用原則式管理來監視和強制最佳做法 |Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 46788407-187e-4b0b-bfe4-529af8d77c60
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 31cd1294590d81c25a0a09d67a7746ea7dee49ea
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="monitor-and-enforce-best-practices-by-using-policy-based-management"></a>使用原則式管理來監視和強制最佳做法
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 原則式管理可讓您監視 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的最佳做法。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會提供一組原則檔讓您當作最佳做法原則匯入，然後為包含執行個體、執行個體物件、資料庫或資料庫物件的目標集評估原則。 您可以手動評估原則、設定原則來根據排程評估目標集，或是設定原則來根據事件評估目標集。 如需原則式管理的詳細資訊，請參閱 [使用原則式管理來管理伺服器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)。  
  
## <a name="policy-and-rules-for-database-engine"></a>Database Engine 的原則和規則  
 下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中所包含的原則，以及有關每一個原則所評估之最佳做法規則的資訊。 這些原則會儲存為 XML 檔案，而且必須匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需如何匯入原則的詳細資訊，請參閱 [匯入原則式管理原則](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md)。  
  
|原則名稱|最佳作法規則|  
|-----------------|------------------------|  
|非對稱金鑰加密演算法|[非對稱金鑰加密強度](../../relational-databases/policy-based-management/asymmetric-keys-encryption-strength.md)|  
|備份和資料檔位置|[備份檔案必須位在與資料庫檔案不同的裝置上](http://msdn.microsoft.com/library/7039bebb-1f25-4cf3-81f1-393dfb78da12)|  
|資料和記錄檔位置|[將資料檔和記錄檔放在不同的磁碟機上](../../relational-databases/policy-based-management/place-data-and-log-files-on-separate-drives.md)|  
|資料庫自動關閉|[將 AUTO_CLOSE 資料庫選項設定為 OFF](../../relational-databases/policy-based-management/set-the-auto-close-database-option-to-off.md)|  
|資料庫自動壓縮|[將 AUTO_SHRINK 資料庫選項設定為 OFF](../../relational-databases/policy-based-management/set-the-auto-shrink-database-option-to-off.md)|  
|資料庫定序|[將使用者定義資料庫的定序設定為 master 和 model 資料庫的定序](http://msdn.microsoft.com/library/c686446f-dae1-4b05-a3df-837b3422988d)|  
|資料庫頁面驗證|[將 PAGE_VERIFY 資料庫選項設定為 CHECKSUM](../../relational-databases/policy-based-management/set-the-page-verify-database-option-to-checksum.md)|  
|資料庫頁面狀態|[檢查具有可疑頁面的資料庫是否完整](../../relational-databases/policy-based-management/check-integrity-of-database-with-suspect-pages.md)|  
|Guest 權限|[使用者資料庫的 Guest 權限](../../relational-databases/policy-based-management/guest-permissions-on-user-databases.md)|  
|上次成功備份日期|[過期的備份](../../relational-databases/policy-based-management/outdated-backup.md)|  
|未對外授予伺服器權限|[伺服器 public 權限](../../relational-databases/policy-based-management/server-public-permissions.md)|  
|SQL Server 64 位元 Affinity Mask 重疊|[Correct Affinity Mask and Affinity Input and Output Mask Overlap](../../relational-databases/policy-based-management/correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|SQL Server Affinity Mask|[保留 Affinity Mask 預設值](../../relational-databases/policy-based-management/keep-the-affinity-mask-default-value.md)|  
|SQL Server 已封鎖的處理序臨界值|[增加或停用 Blocked Process Threshold](../../relational-databases/policy-based-management/increase-or-disable-blocked-process-threshold.md)|  
|SQL Server 預設追蹤|[預設追蹤記錄檔已停用](../../relational-databases/policy-based-management/default-trace-log-files-disabled.md)|  
|SQL Server 動態鎖定|[保留鎖定組態選項預設值](../../relational-databases/policy-based-management/keep-the-locks-configuration-option-default-value.md)|  
|SQL Server 輕量型共用|[停用輕量型共用](../../relational-databases/policy-based-management/disable-lightweight-pooling.md)|  
|SQL Server 登入模式|[選擇驗證模式](../../relational-databases/security/choose-an-authentication-mode.md)|  
|SQL Server 平行處理原則的最大程度|[設定平行處理原則的最大程度選項來取得最佳效能](../../relational-databases/policy-based-management/set-the-max-degree-of-parallelism-option-for-optimal-performance.md)|  
|32 位元 SQL Server 2000 的 SQL Server 最大工作者執行緒|[確認最大工作者執行緒設定](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|64 位元 SQL Server 2000 的 SQL Server 最大工作者執行緒|[確認最大工作者執行緒設定](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|SQL Server 2005 和更新版本的 SQL Server 最大工作者執行緒|[確認最大工作者執行緒設定](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|SQL Server 網路封包大小|[網路封包大小不應超過 8060 個位元組](../../relational-databases/policy-based-management/network-packet-size-should-not-exceed-8060-bytes.md)|  
|SQL Server 密碼逾期|[SQL Server 登入密碼逾期](../../relational-databases/policy-based-management/sql-server-login-password-expiration.md)|  
|SQL Server 密碼原則|[SQL Server 登入密碼強度](../../relational-databases/policy-based-management/sql-server-login-password-strength.md)|  
|使用者資料庫的對稱金鑰加密|[使用者資料庫上的對稱金鑰](../../relational-databases/policy-based-management/symmetric-keys-on-user-databases.md)|  
|master 資料庫的對稱金鑰|[系統資料庫上的對稱金鑰](../../relational-databases/policy-based-management/symmetric-keys-on-system-databases.md)|  
|系統資料庫的對稱金鑰|[系統資料庫上的對稱金鑰](../../relational-databases/policy-based-management/symmetric-keys-on-system-databases.md)|  
|可信任的資料庫|[Trustworthy 位元](../../relational-databases/policy-based-management/trustworthy-bit.md)|  
|Windows 事件記錄檔叢集磁碟資源損毀錯誤|[偵測到 SCSI 主機介面卡問題](../../relational-databases/policy-based-management/detect-scsi-host-adapter-issues.md)|  
|Windows 事件記錄檔裝置驅動程式控制項錯誤|[裝置驅動程式控制項錯誤](../../relational-databases/policy-based-management/device-driver-control-error.md)|  
|Windows 事件記錄檔裝置未就緒錯誤|[裝置未就緒錯誤](../../relational-databases/policy-based-management/device-not-ready-error.md)|  
|Windows 事件記錄檔失敗的 I/O 要求錯誤|[偵測失敗的輸入和輸出要求](../../relational-databases/policy-based-management/detect-failed-input-and-output-requests.md)|  
|Windows 事件記錄檔 I/O 延遲警告|[Check Disk Input and Output Subsystem for IO Delay Problems](../../relational-databases/policy-based-management/check-disk-input-and-output-subsystem-for-io-delay-problems.md)|  
|Windows 事件記錄檔硬分頁錯誤期間的 I/O 錯誤|[硬性分頁錯誤期間的輸入和輸出錯誤](../../relational-databases/policy-based-management/input-and-output-error-during-hard-page-fault.md)|  
|Windows 事件記錄檔讀取重試錯誤|[檢查磁碟輸入輸出子系統的讀取重試問題](../../relational-databases/policy-based-management/check-disk-input-output-subsystem-for-read-retry-problems.md)|  
|Windows 事件記錄檔儲存系統 I/O 逾時錯誤|[儲存體系統輸入輸出逾時](../../relational-databases/policy-based-management/storage-system-input-output-time-out.md)|  
|Windows 事件記錄檔系統失敗錯誤|[非預期的系統失敗](../../relational-databases/policy-based-management/unexpected-system-failures.md)|  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理 Facet](../../relational-databases/policy-based-management/working-with-policy-based-management-facets.md)  
  
  
