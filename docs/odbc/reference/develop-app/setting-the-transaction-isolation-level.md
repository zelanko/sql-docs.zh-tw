---
description: 設定交易隔離等級
title: 設定交易隔離等級 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f871ef9e25cb5745987079a4d94272d2f430dfaf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476410"
---
# <a name="setting-the-transaction-isolation-level"></a>設定交易隔離等級
若要設定交易隔離等級，應用程式會使用 SQL_ATTR_TXN_ISOLATION 的連接屬性。 如果資料來源不支援要求的隔離等級，則驅動程式或資料來源可以設定較高的層級。 為了判斷資料來源支援的交易隔離等級以及預設的隔離等級為何，應用程式會分別使用 SQL_TXN_ISOLATION_OPTION 和 SQL_DEFAULT_TXN_ISOLATION 選項來呼叫 **SQLGetInfo** 。  
  
 較高層級的交易隔離可針對資料庫資料的完整性提供最大的保護。 可序列化交易保證會受到其他交易的影響，因此保證會維持資料庫的完整性。  
  
 不過，較高的交易隔離層級可能會導致效能變慢，因為這樣會增加應用程式必須等候資料鎖定才能釋放的機會。 應用程式可以指定較低層級的隔離，以在下列情況下提高效能：  
  
-   當您可以保證可能會干擾應用程式的交易時，不會有其他交易。 這種情況只會在有限的情況下發生，例如當小型公司的某位人員在一部電腦上維護包含人員資料的 dBASE 檔案，但不共用這些檔案時。  
  
-   當速度比精確度更重要，且任何錯誤可能會很小。 例如，假設某家公司進行了許多小型銷售，而大型銷售很罕見。 估計所有開放式銷售的總計值的交易，可能會安全地使用讀取未認可的隔離等級。 雖然交易會包含正在開啟或已關閉的訂單，並接著回復，但這些訂單通常會彼此取消，而交易的速度會更快，因為它不會在每次遇到這類訂單時遭到封鎖。  
  
 如需詳細資訊，請參閱 [開放式並行](../../../odbc/reference/develop-app/optimistic-concurrency.md)存取。
