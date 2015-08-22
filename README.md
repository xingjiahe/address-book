# address-book

//主函数
#import <Foundation/Foundation.h>
#import "AddressContact.h"
int main(int argc, const char * argv[]) {
    @autoreleasepool {
        
      
        
        
        //联系人初始化
        AddressContact *a1 = [AddressContact setAddressName:@"Abi"number:@"13298897899" gender:@"f" address:@"qqq" age:23 group:@"A"];
        AddressContact *a2 = [AddressContact setAddressName:@"Bing" number:@"13298897897" gender:@"f" address:@"www" age:21 group:@"B"];
        AddressContact *a3 = [AddressContact setAddressName:@"Cing" number:@"13298897895" gender:@"f" address:@"eww" age:22 group:@"C"];

        AddressContact *a4 = [AddressContact setAddressName:@"Deng" number:@"13298897893" gender:@"m" address:@"rrr" age : 25 group:@"D"];

        AddressContact *a5 = [AddressContact setAddressName:@"Eing" number:@"12345" gender:@"f" address:@"zzz" age:23 group:@"E"];

        
        AddressContact *a6 =[AddressContact setAddressName:@"Fing" number:@"13298897891" gender:@"f" address:@"zza" age:23 group:@"F"];
        
        
        AddressContact *a7 = [AddressContact setAddressName:@"Dnng" number:@"13298897873" gender:@"m" address:@"rrr" age : 22 group:@"D"];

        AddressContact *a8 = [AddressContact setAddressName:@"Dang" number:@"1329889122" gender:@"m" address:@"rrr" age : 21 group:@"D"];

        //联系人数组
        NSMutableArray *add = [NSMutableArray arrayWithObjects:a1,a2,a3,a4,a5,a6, a7,a8,nil];
        
        NSMutableArray *AddressCon = [NSMutableArray array];
        //添加联系人
        for (AddressContact *obj in add) { //如果姓名和号码为空则不加入数组(添加失败)
            if ([obj getName] != nil && [obj getNumber] != nil) {
                
                [AddressCon addObject:obj];
            }
        }
        NSLog(@"联系人:%@",AddressCon);

        
        //按照联系人姓名首字母分组
        NSMutableArray *arrayName = [NSMutableArray arrayWithObjects:[NSMutableArray array],[NSMutableArray array],
            [NSMutableArray array],[NSMutableArray array],
            [NSMutableArray array],[NSMutableArray array],
            [NSMutableArray array],[NSMutableArray array],
            [NSMutableArray array],[NSMutableArray array],
            [NSMutableArray array],[NSMutableArray array],
            [NSMutableArray array],[NSMutableArray array],
            [NSMutableArray array],[NSMutableArray array],
            [NSMutableArray array],[NSMutableArray array],
            [NSMutableArray array],[NSMutableArray array],
            [NSMutableArray array],[NSMutableArray array],
            [NSMutableArray array],[NSMutableArray array],
            [NSMutableArray array],[NSMutableArray array],nil];
        
        
        //联系人姓名,群组字典
        NSMutableArray *arraykey = [NSMutableArray arrayWithObjects:@"A",@"B",@"C",@"D",@"E",@"F",@"G",@"H",@"I",@"J",@"K",@"L",@"M",@"N",@"O",@"P",@"Q",@"R",@"S",@"T",@"U",@"V",@"W",@"X",@"Y",@"Z", nil];
        
        NSMutableDictionary *dic = [NSMutableDictionary dictionaryWithObjects:arrayName forKeys:arraykey];
        
        
        
        for (id obj in dic)
        {
            for (int i = 0; i < [AddressCon count]; i++) {
                if ([obj isEqualToString:[AddressCon[i] getGroup]])
                {
                    [dic[obj] addObject:AddressCon[i]] ;
                }
                
            }
        }
        
        NSLog(@"联系人字典:%@",dic);

#if 1
        //D组升序排列
        for (id obj in dic)
        {
            
            if ([obj isEqual: @"D"])
            {
            [dic[obj] sortUsingComparator:^NSComparisonResult(id obj1, id obj2) {
                        return [[obj1 getName]compare:[obj2 getName]];
                    }];

                
                
                NSLog(@"%@",[dic valueForKey:obj]);
            }
        }

        
        //按照电话号码查找练习人
        for (id obj in AddressCon)
        {
            if ([[obj getNumber]isEqualToString:@"13298897897"])
            {
                NSLog(@"联系人是:%@",[obj getName]);
            }
        }
     
        //输出所有女性联系人
        
        NSMutableArray *arr = [NSMutableArray array];
        for (id obj in AddressCon)
        {
            if ([[obj getGender] isEqualToString:@"f"])
            {
             [arr addObject:obj];
                
            }
        }
        [arr sortUsingSelector:@selector(CompareByAge:)];
        NSLog(@"所有女人:%@",arr);
        
        //根据姓名删除某个联系人
        
        
        for (int i = 0; i < [AddressCon count]; i++) {
            if ([[AddressCon[i] getName] isEqual: @"Eing"]) {
                [AddressCon removeObjectAtIndex:i];
            }
        }
        NSLog(@"删除之后:%@",AddressCon);
        
        
        //删除某个分组的全部联系人
        NSArray *arrayKey1 = [dic allKeys];
        for (int i = 0; i < [arrayKey1 count]; i++) {
            if ([arrayKey1[i] isEqualToString:@"B"]) {
                [dic[arrayKey1[i]] removeAllObjects];
            }
        }

        NSLog(@"删除B组联系人后:%@",dic);
#endif
        
    }
    return 0;
}
//联系人类  .m文件
#import "AddressContact.h"

@implementation AddressContact


-(id)initWithName:(NSString *)name number:(NSString*)number gender:(NSString *)gender address:(NSString *)address age:(NSInteger)age group:(NSString *)group
{
    _name = name;
    _number = number;
    _gender = gender;
    _address = address;
    _age = age;
    _group = group;
    return  self;
    
}


+(id)setAddressName:(NSString *)name  number:(NSString *)number gender:(NSString *)gender address:(NSString *)address age:(NSInteger)age group:(NSString *)group
{
    AddressContact *a = [[AddressContact alloc]initWithName:name number:number gender:gender address:address age:age group:group];
    return a;
}




-(void)show
{
    NSLog(@"%@ %@ %@ %@ %ld", _name,_number,_gender,_group,_age);
}

- (NSString *)description
{
    return [NSString stringWithFormat:@"%@ %@ %@ %@ %@ %ld", _name,_number,_gender,_group,_address,_age];
}

-(void)setGroup:(NSString *)group
{
    _group = group;
}

-(void)setName:(NSString *)name
{
    _name = name;
}

-(NSString *)getName
{
    return  _name;
}

-(NSString *)getGroup
{
    return _group;
}
-(NSString *)getNumber
{
    return _number;
}

-(void)setNumber:(NSString *)number
{
    _number = number;
}

-(NSString *)getGender
{
    return _gender;
}

-(NSInteger)getAge
{
    return _age;
}

-(BOOL)CompareByAge:(AddressContact *)address
{
    return  _age < [address getAge];
}


@end


