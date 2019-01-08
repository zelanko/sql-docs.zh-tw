---
title: 使用原則式管理來監視和強制最佳做法 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 46788407-187e-4b0b-bfe4-529af8d77c60
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bfc7cc16c9751ebdf64a8e9cd110547255c944ee
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52758010"
---
# <a name="monitor-and-enforce-best-practices-by-using-policy-based-management"></a>使用原則式管理來監視和強制最佳做法
  以原則為基礎的管理可讓您監視的最佳作法[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會提供一組原則檔讓您當做最佳作法原則來匯入，然後針對包含執行個體、執行個體物件、資料庫或資料庫物件的目標集來評估原則。 您可以手動評估原則、設定原則來根據排程評估目標集，或是設定原則來根據事件評估目標集。 如需原則式管理的詳細資訊，請參閱 [使用原則式管理來管理伺服器](administer-servers-by-using-policy-based-management.md)。  
  
## <a name="policy-and-rules-for-database-engine"></a>Database Engine 的原則和規則  
 下表列出隨附安裝的原則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和包含每個原則評估之最佳作法規則的相關資訊。 這些原則會儲存為 XML 檔案，而且必須匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需如何匯入原則的詳細資訊，請參閱 [匯入原則式管理原則](import-a-policy-based-management-policy.md)。  
  
|原則名稱|最佳作法規則|  
|-----------------|------------------------|  
|非對稱金鑰加密演算法|[非對稱金鑰加密強度](asymmetric-keys-encryption-strength.md)|  
|備份和資料檔位置|[備份檔案必須位在與資料庫檔案不同的裝置上](../../database-engine/backup-files-must-be-on-separate-devices-from-the-database-files.md)|  
|資料和記錄檔位置|[將資料檔和記錄檔放在不同的磁碟機上](place-data-and-log-files-on-separate-drives.md)|  
|資料庫自動關閉|[將 AUTO_CLOSE 資料庫選項設定為 OFF](set-the-auto-close-database-option-to-off.md)|  
|資料庫自動壓縮|[將 AUTO_SHRINK 資料庫選項設定為 OFF](set-the-auto-shrink-database-option-to-off.md)|  
|資料庫定序|[將使用者定義資料庫的定序設定為 master 和 model 資料庫的定序](../../database-engine/set-collation-user-defined-databases-match-master-model-databases.md)|  
|資料庫頁面驗證|[將 PAGE_VERIFY 資料庫選項設定為 CHECKSUM](set-the-page-verify-database-option-to-checksum.md)|  
|資料庫頁面狀態|[檢查具有可疑頁面的資料庫是否完整](check-integrity-of-database-with-suspect-pages.md)|  
|Guest 權限|[使用者資料庫的 Guest 權限](guest-permissions-on-user-databases.md)|  
|上次成功備份日期|[過期的備份](outdated-backup.md)|  
|未對外授予伺服器權限|[伺服器 public 權限](server-public-permissions.md)|  
|SQL Server 32 位元 Affinity Mask 重疊|[正確的 Affinity Mask 和 Affinity 輸入的輸出遮罩重疊](correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|SQL Server 64 位元 Affinity Mask 重疊|[正確的 Affinity Mask 和 Affinity 輸入的輸出遮罩重疊](correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|SQL Server Affinity Mask|[保留 Affinity Mask 預設值](keep-the-affinity-mask-default-value.md)|  
|SQL Server 已封鎖的處理序臨界值|[增加或停用 Blocked Process Threshold](increase-or-disable-blocked-process-threshold.md)|  
|SQL Server 預設追蹤|[預設追蹤記錄檔已停用](default-trace-log-files-disabled.md)|  
|SQL Server 動態鎖定|[保留鎖定組態選項預設值](keep-the-locks-configuration-option-default-value.md)|  
|SQL Server 輕量型共用|[停用輕量型共用](disable-lightweight-pooling.md)|  
|SQL Server 登入模式|[選擇驗證模式](../security/choose-an-authentication-mode.md)|  
|SQL Server 平行處理原則的最大程度|[設定平行處理原則的最大程度選項來取得最佳效能](set-the-max-degree-of-parallelism-option-for-optimal-performance.md)|  
|32 位元 SQL Server 2000 的 SQL Server 最大工作者執行緒|[確認最大工作者執行緒設定](verify-max-worker-threads-setting.md)|  
|64 位元 SQL Server 2000 的 SQL Server 最大工作者執行緒|[驗證最大工作者執行緒設定](verify-max-worker-threads-setting.md)|  
|SQL Server 2005 和更新版本的 SQL Server 最大工作者執行緒|[確認最大工作者執行緒設定](verify-max-worker-threads-setting.md)|  
|SQL Server 網路封包大小|[網路封包大小不應超過 8060 個位元組](network-packet-size-should-not-exceed-8060-bytes.md)|  
|SQL Server 密碼逾期|[SQL Server 登入密碼逾期](sql-server-login-password-expiration.md)|  
|SQL Server 密碼原則|[SQL Server 登入密碼強度](sql-server-login-password-strength.md)|  
|使用者資料庫的對稱金鑰加密|[使用者資料庫上的對稱金鑰](symmetric-keys-on-user-databases.md)|  
|master 資料庫的對稱金鑰|[系統資料庫上的對稱金鑰](symmetric-keys-on-system-databases.md)|  
|系統資料庫的對稱金鑰|[系統資料庫上的對稱金鑰](symmetric-keys-on-system-databases.md)|  
|可信任的資料庫|[Trustworthy 位元](trustworthy-bit.md)|  
|Windows 事件記錄檔叢集磁碟資源損毀錯誤|[偵測到 SCSI 主機介面卡問題](detect-scsi-host-adapter-issues.md)|  
|Windows 事件記錄檔裝置驅動程式控制項錯誤|[裝置驅動程式控制項錯誤](device-driver-control-error.md)|  
|Windows 事件記錄檔裝置未就緒錯誤|[裝置未就緒錯誤](device-not-ready-error.md)|  
|Windows 事件記錄檔失敗的 I/O 要求錯誤|[偵測失敗的輸入的輸出要求](detect-failed-input-and-output-requests.md)|  
|Windows 事件記錄檔 I/O 延遲警告|[檢查磁碟輸入輸出子系統的 IO 延遲問題](check-disk-input-and-output-subsystem-for-io-delay-problems.md)|  
|Windows 事件記錄檔硬分頁錯誤期間的 I/O 錯誤|[硬性分頁錯誤期間的輸入和輸出錯誤](input-and-output-error-during-hard-page-fault.md)|  
|Windows 事件記錄檔讀取重試錯誤|[檢查磁碟輸入輸出子系統的讀取重試問題](check-disk-input-output-subsystem-for-read-retry-problems.md)|  
|Windows 事件記錄檔儲存系統 I/O 逾時錯誤|[儲存體系統輸入輸出逾時](storage-system-input-output-time-out.md)|  
|Windows 事件記錄檔系統失敗錯誤|[非預期的系統失敗](unexpected-system-failures.md)|  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理 Facet](working-with-policy-based-management-facets.md)  
  
  
