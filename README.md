![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 获取大小以GB（数据，日志和总计）为单位的所有数据库大小
#### Get All Database Sizes in GB (Data, Log, and Total) Rounded
**发布-日期: 2015年08月19日 (评论)**

![#](images/##############?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
这里有一些SQL逻辑基本上会以GB为单位提供数据，日志和总数（数据+日志）。另外，所有尺寸均为圆形（天花板）。

用于引用的总计的SQL逻辑需要注意：1GB内的差异舍入为1GB，如果找到的差异少于1GB，则数据和日志文件之间的总数不会超过1GB。 


## English
Here’s some SQL logic that will basically give you the data, log, and total (data + log) in GB. Additionally; all sizes are rounded (ceiling).

SQL logic for totals for reference Note: Variances within 1GB are rounded as 1GB and totals between data & log files will not exceed 1gb if fewer than 1GB variances are found.

---
## Logic
```SQL
use master;
set nocount on
select
[name] = upper(sd.name)
,   [data   - in gb]    = ceiling(sum(case when type = 0 then (smf.size*8)/1024.0/1024.0 else 0 end))
,   [log    - in gb]    = ceiling(sum(case when type = 1 then (smf.size*8)/1024.0/1024.0 else 0 end)) , [total  - in gb]    = ceiling(sum(smf.size * 8.00/1024.00/1024.00)) from
sys.databases sd join sys.master_files smf on sd.database_id = smf.database_id where
sd.source_database_id is null
and sd.name not in ('master', 'model', 'msdb', 'tempdb')
group by
sd.name
order by
[data   - in gb] desc


```



[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

