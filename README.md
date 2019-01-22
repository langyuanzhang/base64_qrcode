# base64_qrcode
TP5生成base64二维码

```
//二维码
public function base_qrcode($order_id,$ordertype)
{	
    vendor("phpqrcode.phpqrcode");
    $level = 'H';// 纠错级别：L、M、Q、H
    $size = 4;// 点的大小：1到10,用于手机端4就可以了
    $QRcode = new \QRcode();
    ob_start();
    $value= $order_id.','.$ordertype; 
    $QRcode->png($value,false,$level,$size,2);
    $imageString = base64_encode(ob_get_contents());  
    ob_end_clean();
    // return "data:image/jpg;base64,".$imageString;
    $datas = ['name'=>'','img_type'=>'base64','savename'=>$imageString,'savepath'=>'data:image/jpg;base64,','order_id'=>$order_id,'order_type'=>$ordertype,'status'=>0];
    Db::name('orde_qrcode')->insert($datas);

    // return '<img src="data:image/png;base64,'.$imageString.'" width="200" height="200">';
}
```