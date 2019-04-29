---
title: 選擇加密演算法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- cryptography [SQL Server], algorithms
- encryption [SQL Server], algorithms
- security [SQL Server], encryption
- algorithms [SQL Server encryption]
ms.assetid: 8227028c-a9c9-489d-bd27-fbf8242634ae
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 853e85ea84b84f1ed0af040be5d8614feab193b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63011388"
---
# <a name="choose-an-encryption-algorithm"></a>選擇加密演算法
  加密是全面防禦中的一環，可提供給想要維護 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體安全的管理員使用。  
  
 加密演算法會定義資料轉換，讓未經授權的使用者無法輕鬆地反轉資料轉換。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可讓管理員和開發人員在數種演算法中進行選擇，包括 DES、Triple DES、TRIPLE_DES_3KEY、RC2、RC4、128 位元 RC4、DESX、128 位元 AES、192 位元 AES 和 256 位元 AES。  
  
 同一種演算法不可能適用於所有情況，各種演算法優缺點的指南也超出《 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》的範疇。 不過，下列為一般適用的原則：  
  
-   強式加密通常比弱式加密耗用更多 CPU 資源。  
  
-   長金鑰通常會比短金鑰產生更強的加密。  
  
-   非對稱加密比使用相同金鑰長度的對稱加密更弱，而且速度相對比較慢。  
  
-   含有長金鑰的區塊密碼比串流式密碼更強。  
  
-   複雜的長密碼比短密碼更強。  
  
-   如果您要加密很多資料，應該使用對稱金鑰來加密資料，並使用非對稱金鑰來加密對稱金鑰。  
  
-   加密的資料無法壓縮，但壓縮資料可以加密。 如果您使用壓縮，應該在加密之前先壓縮資料。  
  
> [!IMPORTANT]  
>  只有 RC4 演算法支援回溯相容性。 只有在資料庫相容性層級為 90 或 100 時，才能使用 RC4 或 RC4_128 加密新資料  (不建議使用)。請改用較新的演算法，例如其中一個 AES 演算法。 在 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和更新版本中使用 RC4 或 RC4_128 加密的資料，可以在任何相容性層級進行解密。  
>   
>  在不同的資料區塊上重複使用相同的 RC4 或 RC4_128 KEY_GUID，結果會是相同的 RC4 金鑰，因為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會自動提供 Salt。 重複使用相同的 RC4 金鑰是已知的錯誤，此錯誤會造成加密變弱。 因此，我們取代了 RC4 和 RC4_128 關鍵字。 [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)]  
  
 如需加密演算法和加密技術的詳細資訊，請參閱 MSDN 上《.NET Framework 開發人員手冊》中的 [重要的安全性概念](https://go.microsoft.com/fwlink/?LinkId=62082) 。  
  
 **釐清有關 DES 演算法的資訊：**  
  
-   DESX 未正確命名。 以 ALGORITHM = DESX 建立的對稱金鑰實際上使用具有 192 位元金鑰的 TRIPLE DES 加密。 未提供 DESX 演算法。 [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   以 ALGORITHM = TRIPLE_DES_3KEY 建立的對稱金鑰使用具有 192 位元金鑰的 TRIPLE DES。  
  
-   以 ALGORITHM = TRIPLE_DES 建立的對稱金鑰使用具有 128 位元金鑰的 TRIPLE DES。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|使用對稱金鑰加密。|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)|  
|使用非對稱金鑰加密。|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)|  
|使用憑證加密。|[CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)|  
|使用透明資料加密來加密資料庫檔案。|[透明資料加密 &#40;TDE&#41;](transparent-data-encryption.md)|  
|如何加密資料表的一個資料行。|[加密資料行](encrypt-a-column-of-data.md)|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 加密](sql-server-encryption.md)   
 [加密階層](encryption-hierarchy.md)  
  
  
