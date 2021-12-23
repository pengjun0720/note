# Java工具类笔记

## 1、关于POI

1.1、java获取单元格任意类型值并转String

```java
public String getCellValue(XSSFCell cell) {
    String value = "";
    // 以下是判断数据的类型
    switch (cell.getCellType()) {
        case HSSFCell.CELL_TYPE_NUMERIC:
            value = cell.getNumericCellValue() + "";
            if (HSSFDateUtil.isCellDateFormatted(cell)) {
                Date date = cell.getDateCellValue();
                if (date != null) {
                    value = new SimpleDateFormat("yyyy-MM-dd").format(date);
                } else {
                    value = "";
                }
            } else {
                value = new DecimalFormat("0").format(cell.getNumericCellValue());
            }
            break;
            // 字符串
        case HSSFCell.CELL_TYPE_STRING:
            value = cell.getStringCellValue();
            break;
            // Boolean
        case HSSFCell.CELL_TYPE_BOOLEAN: 
            value = cell.getBooleanCellValue() + "";
            break;
            // 公式
        case HSSFCell.CELL_TYPE_FORMULA: 
            value = cell.getCellFormula() + "";
            break;
            // 空值
        case HSSFCell.CELL_TYPE_BLANK: 
            value = "";
            break;
            // 故障
        case HSSFCell.CELL_TYPE_ERROR: 
            value = "非法字符";
            break;
        default:
            value = "未知类型";
            break;
    }
    return value;
}
```

