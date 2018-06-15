---
title: 自訂應用程式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9475bc17948e2146493cade0f884cac8885eea62
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908383"
---
# <a name="custom-applications"></a>自訂應用程式
自訂應用程式通常會執行特定工作的幾個 Dbms。 例如，應用程式可能會擷取單一的 DBMS 資料和產生報表，或它可能會傳送數個 Dbms 之間的資料。 什麼這些應用程式有通用是這些 Dbms 已知寫入應用程式之前，不太可能會變更應用程式生命週期。  
  
 自訂應用程式，因此需要少量或沒有互通性。 應用程式開發人員可以針對每個 DBMS 和程式碼直接加入這些驅動程式選擇一個驅動程式。 應用程式可以安全地包含驅動程式專屬程式碼來利用這些驅動程式的功能，而且甚至可能會導致呼叫原生資料庫應用程式開發介面，以使用不支援 ODBC 的功能。  
  
 大部分的自訂應用程式的主要互通性考量是是否目標 Dbms 將在未來變更。 若是如此，可簡化此程序開始撰寫更具互通性程式碼。 不過，這類變更的 Dbms 很少見，而且通常牽涉到大量的工作。 因為這個緣故，自訂應用程式的開發人員很少選擇增加互通性，但會犧牲功能。通常，他們選擇其變更 Dbms 時，重新設定該功能。
