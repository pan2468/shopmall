## ๐ ์ผํ๋ชฐ ํ๋ก์ ํธ
์คํ๋ง ๋ถํธ ์ผํ๋ชฐ ํ๋ก์ ํธ with JPA - ์ ์ ๋ณ๊ตฌํ ์ฑ์ ์ฝ๊ณ  ํด๋ฆฐ์ฝ๋ฉ์ ํ์ฌ, ํ๋ก์ ํธ ์ค์ ๊ณผ ์ผํ๋ชฐ ํ๋ก์ ํธ์ ๋๋ฉ์ธ ๊ตฌ์กฐ ๋๋ ๊ตฌํ๊ณผ์ ์ ๋ํด์ ์์ ์์๊ณ 
์ฐ๊ด ๊ด๊ณ Entity๋ค๋ผ๋ฆฌ ๋ฉ์ธํ๋ฉด, ์ํ๊ด๋ฆฌ, ์ฅ๋ฐ๊ตฌ๋, ๊ตฌ๋งค์ด๋ ฅ ๋ฑ ๋งคํํ์ฌ ์กฐ์ธ์ ๋ํด์๋ ์์ ์์์ต๋๋ค. 

### ๐ ๊ธฐ๋ฅ ์ค๋ช
+ JpaRepository ์ธํฐํ์ด์ค CRUD ๋ฉ์๋ ์ด์ฉํ์ฌ ์ํ๊ด๋ฆฌ, ๊ตฌ๋งค์ด๋ ฅ, ์ฅ๋ฐ๊ตฌ๋ ๊ธฐ๋ฅ ๊ตฌํ
+ QueryDSL ๊ฐ์ฒด์งํฅ ์ฟผ๋ฆฌ๋ฅผ ์ด์ฉํ์ฌ ๊ฒ์์กฐ๊ฑด ๊ตฌํ
+ SpringSecurity ์ค์ 
+ UserDetailsService ๋ก๊ทธ์ธ ์ธ์ฆ ๊ตฌํ

### ๐ ์ ์๊ธฐ๊ฐ, ์ฐธ์ฌ์ธ์
+ ์ ์๊ธฐ๊ฐ: 2022.05.10 ~ 2022.05.15
+ ์ฐธ์ฌ์ธ์: ๊ฐ์ธํ๋ก์ ํธ
### ๐  ์ฌ์ฉ๊ธฐ์  (๊ธฐ์ ์คํ)
+ Java 11
+ SpringBoot 2.7.0
+ Spring Security
+ Spring Data JPA
+ QueryDSL 5.0.0
+ Maven
+ MySQL

## ๐ ์ํ์ค ๋ค์ด์ด๊ทธ๋จ

<img src="https://user-images.githubusercontent.com/58936137/180211415-6fb8869f-1fe0-4dc6-98fb-e76c55b335bf.png" width="800px" height="450px">


## ๐ ์๋น์ค ํ๋ฉด

<details>
<summary><b>์๋น์ค ํ๋ฉด</b></summary>
<div markdown="1">

<details>
<summary><b>๋ก๊ทธ์ธ</b></summary>
<div markdown="2">
	
<img src="https://user-images.githubusercontent.com/58936137/180049925-15194daf-d78d-4402-a48c-30da56db3bb3.png" width="750px" height="450px">

### ๋ก๊ทธ์ธ ์ธ์ฆ
+ email, password ์๋ ฅ์ ํฉ๋๋ค.
+ SpringSecurity ๋ณด์ํ๋ ์์ํฌ์์ UserDetailsService ์ฌ์ฉํ์ฌ ๋ก๊ทธ์ธ ์ธ์ฆ
</div>
</details>

<details>
<summary><b>ํ์ ๊ฐ์</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180049754-499d18ee-37ec-4c2b-91a3-3c869f5b1cd1.png" width="750px" height="450px">

### ํ์๊ฐ์ insert
+ ์ด๋ฆ, ์ด๋ฉ์ผ ์ฃผ์, ๋น๋ฐ๋ฒํธ, ์ฃผ์๋ฅผ ์๋ ฅํฉ๋๋ค.
+ JpaRepository ์ธํฐํ์ด์ค save() ๋ฉ์๋๋ฅผ ์ด์ฉํ์ฌ ๋ฑ๋กํ์ฌ INSERT ์ฝ์ํฉ๋๋ค. 

</div>
</details>

<details>
<summary><b>๋ฉ์ธ ํ์ด์ง</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180047764-3856a741-86e4-4f15-8344-eb117458f4d7.png" width="750px" height="450px">
	
### ๋ฉ์ธํ์ด์ง 
+ ๋ก๊ทธ์ธ ์ธ์ฆ ์ฑ๊ณต์ redirect:/ ๋ฉ์ธ ํ์ด์ง๋ก ์ด๋ํฉ๋๋ค.
+ admin ๋ก๊ทธ์ธ์ ์ํ๋ฑ๋ก, ์ํ๊ด๋ฆฌ ๋ฉ๋ด๊ฐ ๋งํฌ ํธ์ถ์ด ๋ฉ๋๋ค. 
</div>
</details>

<details>
<summary><b>์ํ ๋ฑ๋ก</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180048894-e95a367c-3537-4a1f-a2f8-1072f855e446.png" width="750px" height="450px">
	
### ์ํ INSERT
+ JpaRepository ์ธํฐํ์ด์ค save()๋ฉ์๋ ์ด์ฉํด์ ์ํ๋ช, ๊ฐ๊ฒฉ, ์ฌ๊ณ , ์ํ ์์ธ๋ด์ฉ, ์ด๋ฏธ์ง ํ์ผ์ ์ฝ์ํฉ๋๋ค. 
</div>
</details>

<details>
<summary><b>์ํ ๊ด๋ฆฌ</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180050285-f3118855-a7df-4b9d-8dd5-f0ea1a90e2e6.png" width="750px" height="450px">
	
### ์ํ ๊ด๋ฆฌ ๋ชฉ๋ก ์ถ๋ ฅ
+ JpaRepository ์ธํฐํ์ด์ค findAll() ๋ฉ์๋๋ฅผ ์ด์ฉํ์ฌ ๊ณต์ง์ฌํญ์ ์ํ ์กฐํ ์ถ๋ ฅ
</div>
</details>

<details>
<summary><b>์ฅ๋ฐ๊ตฌ๋</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180050505-1fe08553-d81e-490b-a2bb-14cbf32389b0.png" width="750px" height="450px">
	
### ์ฅ๋ฐ๊ตฌ๋
+ ๋ฉ์ธ ํ์ด์ง ์ํ ์์ธํ๋ฉด์์ ์ฅ๋ฐ๊ตฌ๋ ๋ด๊ธฐ ๋ฒํผ ํด๋ฆญ
+ JpaRepository save() ๋ฉ์๋ ์ด์ฉํ์ฌ ์ฅ๋ฐ๊ตฌ๋ ๋ชฉ๋ก ์ถ๋ ฅ 
</div>
</details>

<details>
<summary><b>๊ตฌ๋งค์ด๋ ฅ</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180050705-1e926b70-604b-4ddb-b2a4-a52d976b2a12.png" width="750px" height="450px">
	
### ๊ตฌ๋งค์ด๋ ฅ
+ ์ฅ๋ฐ๊ตฌ๋ ํ๋ฉด์์ ์ฒดํฌ๋ฐ์ค ํด๋ฆญ ํ ์ฃผ๋ฌธํ๊ธฐ ๋ฒํผ ํด๋ฆญ 
+ JpaRepository save() ๋ฉ์๋ ์ด์ฉํ์ฌ ๊ตฌ๋งค์ด๋ ฅ ๋ชฉ๋ก ์ถ๋ ฅ 
</div>
</details>

</div>
</details>

## ๐ ํต์ฌ ๊ธฐ๋ฅ

<details>
<summary><b>QueryDSL ์ค์ </b></summary>
<div markdown="2">
	
~~~
<dependency>
	<groupId>com.querydsl</groupId>
	<artifactId>querydsl-jpa</artifactId>
</dependency>
<dependency>
	<groupId>com.querydsl</groupId>
	<artifactId>querydsl-apt</artifactId>
</dependency>
~~~

~~~
<plugin>
	<groupId>com.mysema.maven</groupId>
	<artifactId>apt-maven-plugin</artifactId>
	<version>1.1.3</version>
	<executions>
		<execution>
			<goals>
				<goal>process</goal>
			</goals>
			<configuration>
				<outputDirectory>target/generated-sources/java</outputDirectory>
				<processor>com.querydsl.apt.jpa.JPAAnnotationProcessor</processor>
			</configuration>
		</execution>
	</executions>
</plugin>
~~~

#### QueryDSL ์ธํ
	
+ Ctrl + Alt + Shift + S -> Modules -> Sources -> generated-sources ํด๋ฆญ
	
<img src="https://user-images.githubusercontent.com/58936137/180259777-92bd337c-d209-48a3-a7f2-53c19c90bdda.png" width="700px" height="500px">
	
</div>
</details>


<details>
<summary><b>QueryDSL ๊ฐ์ฒด์งํฅ ์ฟผ๋ฆฌ</b></summary>
<div markdown="2">
	
~~~


    private BooleanExpression searchByLike(String searchBy, String searchQuery){

        if(StringUtils.equals("itemNm",searchBy)){
            return QItem.item.itemNm.like("%" + searchQuery + "%");
        }else if(StringUtils.equals("createBy",searchBy)){
            return QItem.item.createBy.like("%" + searchQuery + "%");
        }
        return null;
    }

    @Override
    public Page<Item> getAdminItemPage(ItemSearchDto itemSearchDto, Pageable pageable) {
        QueryResults<Item> results = queryFactory
                .selectFrom(QItem.item)
                .where(regDtsAfter(itemSearchDto.getSearchDateType()),
                        searchSellStatusEq(itemSearchDto.getSearchSellStatus()),
                        searchByLike(itemSearchDto.getSearchBy(),
                                itemSearchDto.getSearchQuery()))
                .orderBy(QItem.item.id.desc())
                .offset(pageable.getOffset())
                .limit(pageable.getPageSize())
                .fetchResults();

        List<Item> content = results.getResults();
        long total = results.getTotal();
        return new PageImpl<>(content, pageable, total);
    }

~~~

~~~
    @Override
    public Page<MainItemDto> getMainItemPage(ItemSearchDto itemSearchDto, Pageable pageable) {

        QItem item = QItem.item;
        QItemImg itemImg = QItemImg.itemImg;

        QueryResults<MainItemDto> results = queryFactory
                .select(
                        new QMainItemDto(
                                item.id,
                                item.itemNm,
                                item.itemDetail,
                                itemImg.imgUrl,
                                item.price)
                )
                .from(itemImg)
                .join(itemImg.item,item)
                .where(itemImg.repimgYn.eq("Y"))
                .where(itemNmLike(itemSearchDto.getSearchQuery()))
                .orderBy(item.id.desc())
                .offset(pageable.getOffset())
                .limit(pageable.getPageSize())
                .fetchResults();

        List<MainItemDto> content = results.getResults();
        long total = results.getTotal();
        return new PageImpl<>(content, pageable, total);
    }
}

~~~
	
</div>
</details>

<details>
<summary><b>์ฐ๊ด ๊ด๊ณ ๋งคํ</b></summary>
<div markdown="2">

### ์ฐ๊ด ๊ด๊ณ ์ผ๋์ผ
+ @Column(name = "member_id")์ @JoinColumn(name = "member_id") ๋งคํํฉ๋๋ค.
+ @OneToOne(fetch = FetchType.LAZY) ์ง์ฐ ๋ก๋ฉ์ ํตํด์ ์ํ๋ ๊ฐ๋ง ์ถ๋ ฅ
	
~~~

import com.shop.constant.Role;
import com.shop.dto.MemberFormDto;
import lombok.Getter;
import lombok.Setter;
import lombok.ToString;
import org.springframework.security.crypto.password.PasswordEncoder;

import javax.persistence.*;

@Entity
@Table(name = "member")
@Getter @Setter
@ToString
public class Member extends BaseEntity{

    @Id
    @Column(name = "member_id")
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String name;

    @Column(unique = true)
    private String email;

    private String password;

    private String address;

    @Enumerated(EnumType.STRING)
    private Role role;

    public static Member createMember(MemberFormDto memberFormDto, PasswordEncoder passwordEncoder){

        Member member = new Member();
        member.setName(memberFormDto.getName());
        member.setEmail(memberFormDto.getEmail());
        member.setAddress(memberFormDto.getAddress());
        String password = passwordEncoder.encode(memberFormDto.getPassword());
        member.setPassword(password);
        member.setRole(Role.ADMIN);
        return member;
    }

}

~~~

~~~

import lombok.Getter;
import lombok.Setter;
import lombok.ToString;

import javax.persistence.*;

@Entity
@Table(name = "cart")
@Getter @Setter
@ToString
public class Cart extends BaseEntity{

    @Id
    @Column(name = "cart_id")
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    @OneToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "member_id")
    private Member member;

    public static Cart createCart(Member member){
        Cart cart = new Cart();
        cart.setMember(member);
        return cart;
    }
}
~~~

### ์ฐ๊ด ๊ด๊ณ ๋ค๋์ผ 
+  @ManyToOne(fetch = FetchType.LAZY) ์ง์ฐ๋ก๋ฉ ํตํด์ ์ฌ๋ฌ Entity์ ์กฐ์ธํ์ฌ ์ถ๋ ฅ
~~~
import com.shop.constant.OrderStatus;
import lombok.Getter;
import lombok.Setter;

import javax.persistence.*;
import java.time.LocalDateTime;
import java.util.ArrayList;
import java.util.List;

@Entity
@Table(name = "orders")
@Getter @Setter
public class Order extends BaseEntity{

    @Id @GeneratedValue
    @Column(name = "order_id")
    private Long id;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "member_id")
    private Member member;

    private LocalDateTime orderDate; //์ฃผ๋ฌธ์ผ

    @Enumerated(EnumType.STRING)
    private OrderStatus orderStatus; //์ฃผ๋ฌธ์ํ

    @OneToMany(mappedBy = "order", cascade = CascadeType.ALL,
                orphanRemoval = true, fetch = FetchType.LAZY)
    private List<OrderItem> orderItems = new ArrayList<>();

//    private LocalDateTime regTime;
//
//    private LocalDateTime updateTime;

    public void addOrderItem(OrderItem orderItem){
        orderItems.add(orderItem);
        orderItem.setOrder(this);
    }

    public static Order createOrder(Member member, List<OrderItem> orderItemList){
        Order order = new Order();
        order.setMember(member);
        for(OrderItem orderItem : orderItemList){
            order.addOrderItem(orderItem);
        }
        order.setOrderStatus(OrderStatus.ORDER);
        order.setOrderDate(LocalDateTime.now());
        return order;
    }

    public int getTotalPrice(){
        int totalPrice = 0;
        for(OrderItem orderItem : orderItems){
            totalPrice += orderItem.getTotalPrice();
        }
        return totalPrice;
    }

    public void cancelOrder(){
        this.orderStatus = OrderStatus.CANCEL;

        for(OrderItem orderItem : orderItems){
            orderItem.cancel();
        }
    }


}
~~~
	

</div>
</details>



   



