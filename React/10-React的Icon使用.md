## Icon

使用 Icon font 官网上的 icon 引入

```jsx
import { createFromIconfontCN } from '@ant-design/icons'
const IconFont createFromIconfontCN({
  scriptUrl: '//at.alicdn.com/t/font_1882712_co33bk4ad1c.js',
})
```



**注意：上传图标时，请给一个合适的名字，并保证单词正确**

```tsx
import React from "react";
import { Space } from "antd";
import Icon from "@/components/Icon";
export default () => (
  <Space>
    <Icon type="icon-check" />
  </Space>
);
```

```tsx
import React from "react";
import { Space } from "antd";
import { useIntl } from "umi";
import styled from "styled-components";
import Icon from "@/components/Icon";

const Delete = styled.div`
  color: palevioletred;
`;

export default () => {
  const { formatMessage } = useIntl();
  return (
    <div>
      <Delete>
        <Space>
          <Icon type="icon-close-circle-fill" size="large" />
          <span>{formatMessage({ id: "delete" })}</span>
        </Space>
      </Delete>

      <Space>
        <Icon type="icon-download" size="large" />
        <span>{formatMessage({ id: "download" })}</span>
      </Space>
    </div>
  );
};
```
