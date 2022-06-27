# smooth
static DISTANCE: f64 = 1.0; //the width we want to enlarge (global static variable)

fn main() {

    let random = vec ![1.0, 9.970000267028809, 85.63346099853516, 4.634969234466553, 90.383056640625, 4.634969234466553, 90.383056640625, 26.468494415283203];
    let mut test =  vec ![1.0, 9.970000267028809, 85.63346099853516, 4.634969234466553, 90.383056640625, 4.634969234466553, 90.383056640625, 26.468494415283203]; // mimic the real scenery
    handle(&mut test);
    acu(&mut test);
    unit(&mut test);
    clock(&mut test);
    finl(&mut test);

    // let a:f64= 9.0;
    //
    // println!("{}",a.sqrt()); // the method of the square root of the specific number.





}
fn finl(mut arr: &mut Vec<f64>) -> Vec<f64> {
    // 回头在这里加一个判断：设置一个初始值
    let arr1 =handle(&mut arr); // first pass the value in:
    // let arr2 =acu(&mut arr);
    let arr2 =clock(&mut arr);// direction
    let arr3 =unit(&mut arr); //hthetal


    // let mut xtd:Vec<f64> = Vec::new(); // 检查是否是同号！ 特意拿中文写的: 千万注意...
    let mut ncdR:Vec<f64> = Vec::new(); //new coordinate(our final work) for right
    let mut ncdL:Vec<f64> = Vec::new(); //new coordinate(our final work) for right
    ncdR.push(85.63346099853516);
    ncdR.push(3.634969234466553);

    ncdL.push(85.63346099853516);
    ncdL.push(5.634969234466553);

    for i in 0..arr2.len(){ // omit the last one

        ncdR.push(arr1[ 2*i+2 ] + arr2 [ i ] *arr3[i][0] );
        ncdR.push(arr1[ 2*i+3 ] + arr2 [ i ] *arr3[i][1] );
        ncdL.push(arr1[ 2*i+2 ] + (-1.0)* arr2 [ i ] *arr3[i][0] );
        ncdL.push(arr1[ 2*i+3 ] + (-1.0)* arr2 [ i ] *arr3[i][1] );

    }
    ncdR.push(91.383056640625);
    ncdR.push(27.468494415283203);
    ncdL.push(89.383056640625);
    ncdL.push(27.468494415283203);

    let mut ncdRa:Vec<f64> = Vec::new(); //right
    let mut ncdRL:Vec<f64> = Vec::new(); //left
    let mut row = 0.2;
    let mut interval = 0.2;

    ncdRa.push(ncdR[0] + 0.2);
    ncdRa.push(ncdR[0 + 1] );
    ncdRa.push(ncdR[0] + 0.4);
    ncdRa.push(ncdR[2 + 1] );

    ncdRa.push(ncdR[4]  );
    ncdRa.push(ncdR[5] -0.4);
    ncdRa.push(ncdR[4]);
    ncdRa.push(ncdR[5] -0.2 );

    ncdRL.push(ncdL[0] + 0.2);
    ncdRL.push(ncdL[0 + 1] );
    ncdRL.push(ncdL[0] + 0.4);
    ncdRL.push(ncdL[2 + 1] );

    ncdRL.push(ncdL[4]  );
    ncdRL.push(ncdL[5 ] -0.4);
    ncdRL.push(ncdL[4] );
    ncdRL.push(ncdL[5] - 0.2 );

    let mut FIN1 :Vec<f64> = Vec::new(); //final

    for i in (0..ncdR.len()-3).filter(|x| x  % 2 ==0 ){
        FIN1.push(ncdRa[i]);
        FIN1.push(ncdRa[i + 1]);
        FIN1.push(ncdRa[i + 2]);
        FIN1.push(ncdRa[i + 3]);

        FIN1.push(ncdRL[i +2 ]);
        FIN1.push(ncdRL[i + 3]);
        FIN1.push(ncdRL[i]);
        FIN1.push(ncdRL[i + 1]);

    }
    let mut gui =   Vec::new();
    for i in (0..15).filter(|x| x  % 8 == 0 ) { //each 4 points has 4 arrow points.
        gui.push(FIN1[i]);
        gui.push(FIN1[i+1]); //because it is double distance
        gui.push(0.009999999776482582);
        gui.push(0.0);
        gui.push(1.0);
        gui.push(9.970000267028809);


        gui.push(FIN1[i + 2]);
        gui.push(FIN1[i + 3] );
        gui.push(0.009999999776482582);
        gui.push(0.0);
        gui.push(0.0);
        gui.push(9.970000267028809);

        gui.push(FIN1[i+4]);
        gui.push(FIN1[i + 5] * DISTANCE);
        gui.push(0.009999999776482582);
        gui.push(1.0);
        gui.push(0.0);
        gui.push(9.970000267028809);

        gui.push(FIN1[i+6]);
        gui.push(FIN1[i + 7]);
        gui.push(0.009999999776482582);
        gui.push(1.0);
        gui.push(1.0);
        gui.push(9.970000267028809);
    }







    let mut FIN :Vec<f64> = Vec::new(); //final

    for i in (0..ncdL.len()-3).filter(|x| x  % 2 ==0 ){
        FIN.push(ncdR[i]);
        FIN.push(ncdR[i + 1]);
        FIN.push(ncdR[i + 2]);
        FIN.push(ncdR[i + 3]);

        FIN.push(ncdL[i + 2]);
        FIN.push(ncdL[i + 3]);
        FIN.push(ncdL[i]);
        FIN.push(ncdL[i + 1]);

    }

    println!("{:?} ncdR is:",ncdR);
    println!("{:?} ncdL is:",ncdL);
    println!("{:?} fin:",FIN);
    println!("{:?} fin1:",FIN1);
    println!("{:?} gui:",gui);
    println!("{:?} ncdRa:",ncdRa);
    println!("{:?} ncdRl:",ncdRL);


    let mut arf :Vec<f64> = Vec::new();
    arf.push(0.2784); // RBG color index, which is fixed
    arf.push(0.2784);
    arf.push(0.2784);
    for i in (0..FIN.len()-1).filter(|x| x % 2 ==0 ){
        arf.push(FIN[i]);
        arf.push(FIN[i+1]); // add the new coordinate into the matrix
        arf.push(0.009999999776482582);// all of the rest are fixed number
        arf.push(0.0);
        arf.push(0.0);
        arf.push(1.0);
        arf.push(0.3411764705882353);
        arf.push(0.5058823529411764);
        arf.push(1.0);
        arf.push(9.970000267028809);


    }
    println!("{:?}arf :",arf);

    FIN

}
//

fn handle(arr: &Vec<f64>) -> Vec<f64> { // handle the vector in order to cut off the former two. // it was used to add return type.
    let mut hdv:Vec<f64> = Vec::new(); //
    // let mut hdv1:Vec<f64> = Vec::new();
    for i in 2..arr.len(){
        hdv.push(arr[i]);


    }


    println!("{:?} data cut is:",hdv);


    hdv

}


fn unit(mut arr: &mut Vec<f64>) -> Vec<Vec<f64>>{ // remember to change it
    let arr1 =handle(&mut arr); // first pass the value in:

    let width = 2;
    let height = arr1.len()/2;

    let mut unitD:Vec<Vec<f64>> = vec![vec![0.0; width ]; height];  // unit direction calculation

    for i in (0..arr1.len()-1).filter(|x| x % 2 ==0){

        unitD[i/2][0] = arr1[i];
        unitD[i/2][1] = arr1[i + 1];


    }

    let width1 = 4;
    let height1 = arr1.len()/2-1;
    let mut unitD1:Vec<Vec<f64>> = vec![vec![0.0; width1 ]; height1]; //set every two points as a group.

    for i in 0..unitD.len()-1 {
        unitD1[i][0] = unitD[i][0];
        unitD1[i][1] = unitD[i][1];
        unitD1[i][2] = unitD[i+1][0];
        unitD1[i][3] = unitD[i+1][1];


    }
    let mut mod1:Vec<f64> = Vec::new();// thr distance between two points.

    for i in 0..unitD1.len(){

        mod1.push( ((unitD1[i][2]  -unitD1[i][0] )* (unitD1[i][2]  -unitD1[i][0] ) + (unitD1[i][3]
            -unitD1[i][1]) *(unitD1[i][3]
            -unitD1[i][1])).sqrt());
    }

    let width2 = 4;
    let height2 = arr1.len()/2;
    let mut unitD2:Vec<Vec<f64>> = vec![vec![0.0; width2 ]; height2]; //set every two points as a group.
    // that is the calculation of the vector
    for i in 0..unitD1.len()-1{

        unitD2[i][0] = ( unitD1[i][0] - unitD1[i][2] ) /  mod1[i];
        unitD2[i][1] = ( unitD1[i][1] - unitD1[i][3] ) /  mod1[i];
        unitD2[i][2] = ( unitD1[i+1][2] - unitD1[i+1][0] ) /  mod1[i+1];
        unitD2[i][3] = ( unitD1[i+1][3] - unitD1[i+1][1] ) /  mod1[i+1]; // please remember this is different

    }
    let mut unitD4:Vec<Vec<f64>> = vec![vec![0.0; width ]; height2];
    for i in 0..unitD2.len(){
        if  (unitD2[i][0] + unitD2[i][2] ==0.0) && (unitD2[i][1] + unitD2[i][3] == 0.0){

            unitD4[i][0] = unitD2[i][1] ;
            unitD4[i][1] = -unitD2[i][0] ;


        }else{
            unitD4[i][0] = unitD2[i][0] + unitD2[i][2];
            unitD4[i][1] = unitD2[i][1] + unitD2[i][3];
        }


    }


    let mut unitD3:Vec<Vec<f64>> = vec![vec![0.0; width2 ]; height2]; //set every two points as a group.
    // that is the calculation of the vector
    for i in 0..unitD1.len()-1{

        unitD3[i][0] = ( unitD1[i][0] - unitD1[i][2] ) ;
        unitD3[i][1] = ( unitD1[i][1] - unitD1[i][3] );
        unitD3[i][2] = ( unitD1[i+1][2] - unitD1[i+1][0] );
        unitD3[i][3] = ( unitD1[i+1][3] - unitD1[i+1][1] ) ; // please remember this is different

    }
    let mut theta:Vec<f64> = Vec::new(); // calculate half the angle

    let width3 = 2;
    let height3 = arr1.len()/2;
    let mut hthetal:Vec<Vec<f64>> = vec![vec![0.0; width3 ]; height3]; // calculate multiply of the original coordinate.

    for i in 0..unitD2.len()-1{


        theta.push( ((((unitD2[i][0]* unitD2[i][2])+( unitD2[i][1]* unitD2[i][3]) )).acos()) / 2.0 );
        //half the angle
        // hthetal[i][0] = (unitD4[i][0]*( DISTANCE)/ (theta[i].tan())) ;
        // hthetal[i][1] = (unitD4[i][1]*( DISTANCE)/ (theta[i].tan()) );
    }
    for i in 0..unitD2.len()-1{
        if theta[i] ==  1.5707963162581844{
            hthetal[i][0]=  (unitD4[i][0]* DISTANCE);
            hthetal[i][1]=  (unitD4[i][1]* DISTANCE);
        }else{
            hthetal[i][0] = (unitD4[i][0]*( DISTANCE)/ (theta[i].tan())) ;
            hthetal[i][1] = (unitD4[i][1]*( DISTANCE)/ (theta[i].tan()) );
        }

    }
    let mut endp:Vec<Vec<f64>> = vec![vec![0.0; width3 ]; height3];
    let mut len = arr1.len() ;
    let mut len1 = mod1.len() ;
    endp[0][0]=(unitD2[0][1]);
    endp[0][1]=(- unitD2[0][0]);
    endp[1][0] = ((arr1[len-1]-arr1[len-3])/mod1[len1-1]);
    endp[1][0] =(-(arr1[len-2]-arr1[len-4])/mod1[len1-1]);




    println!("{:?}",unitD);
    println!("{:?}d1",unitD1);
    println!("{:?}mod1",mod1);
    println!("{:?}d2",unitD2);
    println!("{:?}d3", unitD3);
    println!("{:?}d4", unitD4);
    println!("{:?}theta",theta);
    println!("{:?}h1", hthetal);
    println!("{:?}endp", endp);
    hthetal

}




fn clock(mut arr: &mut Vec<f64>) -> Vec<f64>{
    let arr1 =handle(&mut arr); // first pass the value in:

    let width2 = 4;
    let height2 = arr1.len()/2-2;
    let mut unitD6:Vec<Vec<f64>> = vec![vec![0.0; width2 ]; height2]; //set every two points as a group.
    // that is the calculation of the vector
    for i in (0..arr1.len()-4).filter(|x| x % 2 ==0){

        unitD6[i/2][0] = ( arr1[i+2] - arr1[i] ) ;
        unitD6[i/2][1] = ( arr1[i+3] - arr1[i+1]  ) ;
        unitD6[i/2][2] = ( arr1[i+4] - arr1[i+2] ) ;
        unitD6[i/2][3] = ( arr1[i+5] - arr1[i+3]  ) ;
       // process the cross multiply

    }
    let mut clo:Vec<f64> = Vec::new();
    for i in 0..unitD6.len(){
        if unitD6[i][0]*unitD6[i][3] - unitD6[i][1]*unitD6[i][2] <= 0.0{ //clockwise
            clo.push(1.0 );

        }else{
            clo.push(-1.0 );
        }

    }

    println!("{:?}d6",unitD6);
    println!("{:?}clock",clo);
    clo



}

fn acu(mut arr: &mut Vec<f64>) -> Vec<f64> {
    let arr1 =handle(&mut arr); // first pass the value in:

    let mut direction_y = Vec::new(); // <1,-1> or something like that
    let mut direction_x = Vec::new(); // <1,-1> or something like that


    for i in (1..arr1.len()-1).filter(|x| x%2 ==1){
        if arr1[i+2] > arr1[i] {
            direction_y.push(1.0);
        } else {
            direction_y.push(-1.0);

        }
    }//obtain the direction array:
    println!("{:?}diy",direction_y);

    for i in (0..arr1.len()-2).filter(|x| x%2 ==0){
        if arr1[i+2] > arr1[i] {
            direction_x.push(1.0);
        } else {
            direction_x.push(-1.0);

        }
    }//obtain the direction array:
    println!("{:?} dix" ,direction_x);
    println!("{:?}arr1",arr1);

    direction_y
    // direction_x

}

// remember that the matrix[i] (first coordinate, then the broder line)

// fn smooth(mut arr: &mut Vec<f64>) -> Vec<f64>{ //realise it as flat as possible
//
//
// }
