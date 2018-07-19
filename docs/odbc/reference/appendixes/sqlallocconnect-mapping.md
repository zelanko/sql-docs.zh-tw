---
title: SQLAllocConnect 對應 |Microsoft 文件
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
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1f2485112213bb3b4168bc72f96cee353cd1101
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908083"
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 對應
當應用程式呼叫**SQLAllocConnect**透過 ODBC 3。*x*驅動程式，會呼叫**SQLAllocConnect**(*henv*， *phdbc*) 會對應至**SQLAllocHandle** ，如下所示：  
  
1.  驅動程式管理員配置的連接，並傳回至應用程式。  
  
2.  當應用程式建立連接時，驅動程式管理員呼叫  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     在驅動程式搭配*InputHandle*設*henv*，和*OutputHandlePtr*設*phdbc*。
