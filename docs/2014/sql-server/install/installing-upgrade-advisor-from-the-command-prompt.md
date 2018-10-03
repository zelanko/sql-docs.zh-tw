---
title: 從命令提示字元安裝 Upgrade Advisor |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- command prompt [Upgrade Advisor]
- Setup [Upgrade Advisor]
- Upgrade Advisor [SQL Server], installing
ms.assetid: a6841cc2-ca13-4b1c-9343-9e4d54312c3a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7e834cb85458b7fd0e265e5077500ebc4dec5f45
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095408"
---
# <a name="installing-upgrade-advisor-from-the-command-prompt"></a>從命令提示字元安裝 Upgrade Advisor
  您可以使用安裝精靈或命令提示字元來安裝 Upgrade Advisor。 藉由使用命令提示字元，可執行自主式且自動化的安裝。  
  
## <a name="installation-syntax"></a>安裝語法  
 從命令提示字元安裝 Upgrade Advisor 的基本語法如下：  
  
 `SQLUA.msi [options]`  
  
 下表顯示最常用的選項。  
  
|引數|描述|  
|--------------|-----------------|  
|/q [n&#124;b&#124;r&#124;f]|設定使用者介面 (UI) 層級：<br /><br /> n = 沒有 UI<br /><br /> b = 基本 UI (只有進度，沒有提示)<br /><br /> r = 縮減 UI (在安裝結尾顯示對話方塊)<br /><br /> f = 完整 UI|  
|/L|指定記錄檔選項。 若要記錄所有訊息都*log_file_name*，使用 **-L\*v * * * log_file_name*。 若要記錄僅錯誤訊息，請使用`-Le` *log_file_name*。|  
|ADDLOCAL = ALL&AMP;#124;移除 = ALL&AMP;#124;REINSTALL = ALL|指定要安裝 (ADDLOCAL)、移除 (REMOVE) 或重新安裝 (REINSTALL) Upgrade Advisor。|  
|UAINSTALLDIR=path|將 Upgrade Advisor 安裝至 path 指定的位置。|  
  
## <a name="installation-examples"></a>安裝範例  
 下列範例將示範如何使用命令提示字元來安裝 Upgrade Advisor：  
  
```  
SQLUA.msi /qn ADDLOCAL=ALL UAINSTALLDIR="C:\Upgrade Advisor"  
```  
  
 當您執行此命令時，也可以使用 Msiexec 程式：  
  
```  
Msiexec.exe /i C:\Downloads\SQLUA.msi /qn ADDLOCAL=ALL UAINSTALLDIR="C:\Upgrade Advisor"  
```  
  
 如果您必須使用其他安裝選項，這樣做就很有用。  
  
## <a name="removal-examples"></a>移除範例  
 下列範例將示範如何使用命令提示字元來移除 Upgrade Advisor：  
  
```  
SQLUA.msi /qn REMOVE=ALL  
```  
  
 當您執行此命令時，也可以使用 Msiexec 程式：  
  
```  
Msiexec.exe /i C:\Downloads\SQLUA.msi /qn REMOVE=ALL  
```  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Upgrade Advisor](../../../2014/sql-server/install/installing-upgrade-advisor.md)   
 [升級建議程式必要條件](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
