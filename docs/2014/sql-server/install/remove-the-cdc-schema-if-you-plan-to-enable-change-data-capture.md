---
title: 如果您打算啟用異動資料擷取，請移除 cdc 結構描述 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cc580a6032a19eb8248759669278f8730fc617cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092953"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>如果您計畫啟用異動資料擷取，請移除 cdc 結構描述
  資料庫已經包含 cdc 結構描述。 如果您計畫在升級之後啟用異動資料擷取，就必須先卸除此 cdc 結構描述。 當您啟用異動資料擷取的資料庫時，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 將會建立名為 cdc 的新結構描述。  
  
  
