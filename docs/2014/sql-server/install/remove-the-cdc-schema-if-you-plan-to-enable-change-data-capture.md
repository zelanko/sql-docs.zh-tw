---
title: 如果您計畫啟用異動資料擷取，請移除 cdc 結構描述 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cf7a9173e268b35f5a0a567a0812dc0e0b48ae91
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134324"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>如果您計畫啟用異動資料擷取，請移除 cdc 結構描述
  資料庫已經包含 cdc 結構描述。 如果您計畫在升級之後啟用異動資料擷取，就必須先卸除此 cdc 結構描述。 當您啟用異動資料擷取的資料庫時，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 將會建立名為 cdc 的新結構描述。  
  
  