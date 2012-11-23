
#Php Module Curl

* curl_init
* curl_setopt
* curl_setopt_array
* curl_exec
* culr_getinfo
* curl_close


<pre>
$ch = curl_init('http://www.haozu.com');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_BINARYTRANSFER, true);
$result = curl_exec($ch);
$info = curl_getinfo($ch);
</pre>

##multi 
* curl_multi_select
* curl_multi_getcontent
* curl_multi_info_read
* curl_multi_init
* curl_multi_add_handle
* curl_multi_exec
* curl_multi_remove_handler
* curl_multi_close
<pre>
$nodes = array('http://www.php.net', 'http://www.weibo.com', 'http://www.haozu.com');
$node_count = count($nodes);
$curl_arr = array();
$master = curl_multi_init();
for($i = 0; $i < $node_count; $i++)
{
    $url =$nodes[$i];
    $curl_arr[$i] = curl_init($url);
    curl_setopt($curl_arr[$i], CURLOPT_RETURNTRANSFER, true);
    curl_multi_add_handle($master, $curl_arr[$i]);
}
do {
    curl_multi_exec($master,$running);
    $info = curl_multi_info_read($master);
    print_r($info);

} while($running > 0);
echo "results: ";
for($i = 0; $i < $node_count; $i++)
{
    $results = curl_multi_getcontent  ( $curl_arr[$i]  );
    echo( $i . "\n" . $results . "\n");
}
var_dump(curl_multi_info_read($master));
echo 'done';
</pre>
