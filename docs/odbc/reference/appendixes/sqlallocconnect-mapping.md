---
title: SQLAllocConnect 對應 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65c23f41ea9176c460c8fb32ece5e74dfb803541
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68065018"
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 對應
當應用程式透過 ODBC 3 呼叫**SQLAllocConnect**時。*x*驅動程式，對**SQLAllocConnect**（*henv*， *Phdbc*）的呼叫會對應到**SQLAllocHandle** ，如下所示：  
  
1.  驅動程式管理員會配置連接，並將它傳回給應用程式。  
  
2.  當應用程式建立連接時，驅動程式管理員會呼叫  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     在驅動程式中，將*InputHandle*設定為*henv*，並將*OutputHandlePtr*設定為*phdbc*。
