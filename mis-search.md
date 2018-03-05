# 搜索组件使用说明


> 为了规范搜索区域编码而封装的公共搜索组件 

#### **特点**
- 样式支持自适应
- 可单独设置搜索条件默认展开（收起）
- 默认接受url参数填充表单
- 支持表单类型：单行(多行)文本框、下拉列表、datetimepicker、select2


----------
## **Input**
| Name         | Type         | Default  | Description         |
| :----------- | :----------- | :------- | :------------------ |
| inputOption      | ```InputModel```  | ```null```     | [详情参考此处](#1)    |

## **Output**
| Name         | Parameters   | Description        |
| :----------- | :----------- | :----------------  | 
| urlParams    | queryParams      | url参数 |


----------


## **代码示例**

### Template

```
<mis-search [options]="inputOption" (urlParams)="getUrlParams($event)"></mis-search>
```

### Component

```
import {
  DateTimePickerInputMode, DropDownInputMode,
  InputModel
} from "../../shared/components/mis-search/mis-search.model";

Component({
  selector: 'mis-list',
  templateUrl: './list.component.html',
  styleUrls: ['./list.component.scss']
})

export class DemoListComponent implements{
 inputOption: Array<InputModel> = [
    {
      inputName: 'id',
      placeholder: 'ID',
      label: this.urlParams.getInputLabel('id'),
      type: 'text',
    },
    {
      inputName: 'orderType',
      placeholder: '业务类型',
      label: this.urlParams.getInputLabel('orderType'),
      inputSetting: <DropDownInputMode>{
        dropDownData: this.dictionary.getItems('orderType')
      },
      type: 'dropDown',
    },
    {
      inputName: 'ids',
      placeholder: '策略ID批次，以逗号分割',
      label: this.urlParams.getInputLabel('ids'),
      hidden: true,
      type: 'textarea',
    },
    {
      inputName: 'startTime',
      placeholder: '开始时间',
      label: '开始时间',
      hidden: true,
      inputSetting: <DateTimePickerInputMode>{
        pickerOpt: {
          single: true,
          startDate: "",
          format: 'YYYY-MM-DD',
          timePicker: true,
        },
      },
      type: 'dateTimePicker'
    }
  ]
}
```

###  Model
<p id=1></p>

#### 1. InputModel 

```
export interface InputModel {
  type: string;               // 表单类型：text,textarea,dropDown,dateTimePicker
  inputSetting?: any;         // 针对不同表单，不同设定 
  inputName?: string;         // 表单提交字段
  label?: string;
  placeholder?: string; 
  inputType?: string;         // 表单type属性
  data?: any;                 // 表单数据
  hidden?: boolean;           // true：默认收起
}
```

<p id=2></p>

#### 2. DateTimePickerInputMode

```
export interface DateTimePickerInputMode {
  pickerOpt: any;             // 时间插件设定
}
```


---------
### 提示
如果 ```type='dropDown'``` ，只有在公共字典里 **`定义该字段的字典`**  ，下拉框列表才能显示


