---
title: MSSQLSERVER_33085 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 33085 (Database Engine error)
ms.assetid: c27b8d1d-668a-4ba8-8b61-25a5ebbc5485
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 2d66231f97869207fdc8334b85d9f5d4d24e0183
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022403"
---
# <a name="mssqlserver33085"></a>MSSQLSERVER_33085
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|33085|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SEC_CRYPTOPROVE_METHOD_CANNOT_FOUND|  
|訊息文字|在密碼編譯提供者程式庫 '%.*ls' 中找不到一個或多個方法。|  
  
## <a name="explanation"></a>說明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法使用錯誤訊息中所列的密碼編譯提供者。 此密碼編譯提供者不支援所需的方法。 錯誤的狀態表示找不到哪一個方法。  
  
|State|描述|  
|-----------|-----------------|  
|@shouldalert|SqlCryptInitializeProvider|  
|2|SqlCryptFreeProvider|  
|3|SqlCryptOpenSession|  
|4|SqlCryptCloseSession|  
|5|SqlCryptGetProviderInfo|  
|6|SqlCryptGetNextAlgorithmId|  
|7|SqlCryptGetAlgorithmInfo|  
|8|SqlCryptCreateKey|  
|9|SqlCryptDropKey|  
|10|SqlCryptGetNextKeyId|  
|11|SqlCryptGetKeyInfoByKeyId|  
|12|SqlCryptGetKeyInfoByThumb|  
|13|SqlCryptGetKeyInfoByName|  
|14|SqlCryptExportKey|  
|15|SqlCryptImportKey|  
|16|SqlCryptEncrypt|  
|17|SqlCryptDecrypt|  
  
## <a name="user-action"></a>使用者動作  
 如需詳細資訊，請連絡密碼編譯提供者。  
  
  