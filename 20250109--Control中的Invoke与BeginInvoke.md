## 参考文章
[博客园](https://www.cnblogs.com/ybqjymy/p/14281286.html)

## 大致内容
![alt text](assets/20250109--Control中的Invoke与BeginInvoke/image.png)
![alt text](assets/20250109--Control中的Invoke与BeginInvoke/image-1.png)
![alt text](assets/20250109--Control中的Invoke与BeginInvoke/image-2.png)
```CSharp
// 示例1
delegate void SafeSetText(string strMsg);
private void SetText2(string strMsg)
{
　　SafeSetText objSet = delegate(string str)
   {
       textBox1.Text = str;
   }
   textBox1.Invoke(objSet,new object[]{strMsg});
}
// 示例2
Invoke(() =>
{
    button.Text="关闭";
});
```