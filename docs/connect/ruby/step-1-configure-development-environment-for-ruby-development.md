---
title: 步驟 1： 設定適用於拼音開發的開發環境 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb14bee9528ad23b212bb0a7ffbbba02e1c39678
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35309697"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>步驟 1： 設定適用於拼音開發的開發環境
您必須設定開發環境的必要條件，才能開發使用 SQL Server 的 Ruby 驅動程式的應用程式。    
  
請注意 Ruby 驅動程式會使用 TDS 通訊協定，SQL Server 和 Azure SQL Database 中的預設會啟用。  不需要進行其他組態設定。  
  
  
## <a name="windows"></a>Windows  
  
1.  **下載後安裝程式**  
如果您的電腦沒有 Ruby 請加以安裝。 新的拼音使用者，我們建議您針對使用拼音 2.2.X 安裝程式。 這些資料行會提供穩定的語言和廣泛的封裝 （珍貴） 相容，並且更新清單。 移[拼音下載頁面](http://rubyinstaller.org/downloads/)及下載適當的 2.1.x 版安裝程式。 如範例中，如果您是在 64 位元的電腦，下載 Ruby 2.1.6 (x64) 安裝程式。   
  
2.  **安裝 Ruby**  
安裝程式下載後，執行下列作業：  
A. 按兩下檔案以啟動安裝程式。  
B. 選取語言，並同意這些條款。  
c.  在 [安裝設定] 畫面中，選取這兩個新增 Ruby 可執行檔路徑和關聯需要.rb 和.rbw 檔案這拼音項安裝旁邊的核取方塊。  
  
3.  **下載拼音 DevKit**  
從 RubyInstaller 頁面下載 DevKit  
  
4.  **安裝拼音 DevKit**  
下載完成之後，執行下列作業：  
A. 按兩下該檔案。 將會要求您解壓縮檔案的位置。  
B. 按一下"..."按鈕，然後選取 「 C:\DevKit"。 您可能必須先建立這個資料夾，依序按一下 建立新資料夾 」。  
c. 按一下 [確定]，並接著 「 擷取 」，請將檔案解壓縮。  
  
5. **開啟 cmd.exe**  
  
6. **初始化拼音 DevKit**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **安裝 TinyTDS 健身**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **開啟終端機**  
  
2. **安裝 Ruby 版本管理員 (rvm) 和必要條件**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **用於安裝 Ruby rvm**  
例如，安裝新版 2.3.0 Ruby:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;請確定最後一個命令的輸出，表示您正在執行版本 2.3.0。  
  
4.  **安裝 freetds 才能使用**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **安裝 TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
請注意，Mac OS X 已經 Ruby 預先安裝，因為 OS 具有相依性。    
  
1.  **開啟終端機**  
  
2. **安裝 Homebrew 封裝管理員**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **安裝 freetds 才能使用**  
```  
> brew install FreeTDS  
```  
  
4.  **安裝 TinyTDS 健身**  
```  
> gem install tiny_tds  
```
