

# 修改记录
- 启用四码上屏
 - `_jde_mod.base.yaml`文件中：`max_code_length: 4`
- 修改`orq`输出
 - `lua/shijian.lua`文件中：
```lua
    -- **日期候选项**
    if (input == "/rq" or input == "orq") then
        local num_year = os.date("%j/") .. IsLeap(os.date("%Y"))
        local date_variants = {
            {os.date("_%Y%m%d.%H%M"), num_year},
            {os.date("%Y-%m-%d"), num_year},
            {os.date("%Y/%m/%d"), num_year},
            {os.date("%Y.%m.%d"), num_year},
            {os.date("%Y年%m月%d日"), num_year},
            {string.gsub(os.date("%m/%d/%Y"), "([^%d])0+", "%1"), num_year},
            {CnDate_translator(os.date("%Y%m%d")), num_year},
            {lunarJzl(os.date("%Y%m%d%H")), " "},
            {Date2LunarDate(os.date("%Y%m%d")) .. JQtest(os.date("%Y%m%d")), ""},
            {Date2LunarDate(os.date("%Y%m%d")) .. GetLunarSichen(os.date("%H"), 1), ""}
        }
        generate_candidates("date", seg, date_variants)
```
