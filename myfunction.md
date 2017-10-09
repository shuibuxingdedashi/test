创建一个json错误信息{#test}
##### 创建一个JSON格式的正确信息
```ruby
 /**
     * 创建一个JSON格式的正确信息
     *
     * @access  protected
     * @param   string  $msg
     * @return  void
     */
    protected function make_json_result($message, $data=array())
    {
    	$result = array(
    			'code' => 0,
    			'msg' => $message,
                'data' => $data,
    		);
    	$str =  json_encode($result);
        $str = str_replace('null', '""', $str);
        $str = str_replace('\\\\', '/', $str);
        echo $str;
        exit;
    }
```

#### 创建一个json错误信息(#test)
```ruby
/**
     * 创建一个JSON格式的错误信息
     *
     * @access  protected
     * @param   string  $msg
     * @return  void
     */
    protected function make_json_error($message = '', $code, $data=array())
    {
    	$result = array(
    			'code' => $code,
    			'msg' => $message,
    			'data' => $data,
    		);
    	$str =  json_encode($result);
        $str = str_replace('null', '""', $str);
        $str = str_replace('\\\\', '/', $str);

        echo $str;
        exit;
    }
```
### 递归重组节点信息为多维数组
```Ruby
/**
     * 递归重组节点信息为多维数组
     *
     * @param array  $node 
     * @param number $pid   父级id起始值
     * @param string $id_name ID字段名称
     * @param string $pid_name 父ID字段名称
     * @param string $child_name  子集字段名称
     * @author rainfer <81818832@qq.com>
     */
  function tree(&$node, $pid = 0, $id_name = 'id', $pid_name = 'pid', $child_name = '_child')
    {
      $arr = array();

        foreach ($node as $v) {
            if ($v[$pid_name] == $pid){
                $v[$child_name] = tree($node, $v[$id_name], $id_name, $pid_name, $child_name);
                $arr[] = $v;
            } 
        }
        return $arr;
    }
```

### 二维数组按某个值分组
```

/**二维数组按某个值分组
    *@param $arr array 要分组的二维数组
    *@param $key string 分组依据，即key名称
    *@return $array array  三维数组
    */

 function adsp_group($arr, $key){
        
        $grouped = [];

        foreach ($arr as $value) {
            $grouped[$value[$key]][] = $value;
        }

        if (func_num_args() > 2) {

            $args = func_get_args();
            foreach ($grouped as $key => $value) {
                $parms = array_merge([$value], array_slice($args, 2, func_num_args()));
                $grouped[$key] = call_user_func_array('array_group_by', $parms);
            }
        }

        return $grouped;
        
    }  
```
### 对象转数组
```ruby
    /**
     * 对象 转 数组
     *
     * @param object $obj 对象
     * @return array
     */
     function object_to_array($obj) {
        $obj = (array)$obj;
        foreach ($obj as $k => $v) {
            if (gettype($v) == 'resource') {
                return;
            }
            if (gettype($v) == 'object' || gettype($v) == 'array') {
                $obj[$k] = (array)object_to_array($v);
            }
        }

        

        return $obj;
    }
```
    
[### implode自定义函数处理多维数组]



```ruby
/**
 * [php implode自定义函数处理多维数组]
 * @author tianzehui 2017-08-07
 * @param  [array]  $array [多维数组]
 * @param  [string]  $mode  [分割的界定符]
 * @return [string]         [返回的字符串]
 */
public function implode_multiArr($array,$mode)
{
	$dataStr = '';
  foreach( $array as $keys => $values )
   {

	   if( is_array( $values ) )
	   {
	    $dataStr .= $this->implode_multiArr( $values, $mode );
	   }
	   else
	   { 
   		$dataStr .= $values . $mode;
		} 
	}  

  	return $dataStr ;
 }
```
### 去掉字符型串最后一个字符
```ruby
substr($parts_type,0,strlen($parts_type)-1);
```
### 获取唯一订单编号,生成订单使用
```ruby
function create_order_unique($shop_id)
{
    $time = microtime(true);

    list($s1,$s2) = explode('.', $time);

    $order_unique = $shop_id . date("YmdHis") . $s2 . rand(1000,9999);

    return $order_unique;
}
```
  

### 统一支付订单号,生成订单使用

 ```ruby
 
    function create_order_no()
    {
        $time = microtime(true);
        list($s1,$s2) = explode('.', $time);
        $order_no = $s1. $s2 . rand(1000,9999);
        return $order_no;
    }
    
```
### 生成支付单号

    function create_pay_no()
    {
        $time = microtime(true);
        list($s1,$s2) = explode('.', $time);
    
        $pay_no = rand(1000000,99999999).date("YmdHis") . $s2 . rand(100000,999999);
        return $pay_no;
    }
    
### [截取字符](#subtext)
    function subtext($text, $length)
    {
        if(mb_strlen($text, 'utf8') > $length)
            return mb_substr($text, 0, $length, 'utf8').'...';
        return $text;
    }
    
0. 目录{#index}
跳转到[目录](#index)