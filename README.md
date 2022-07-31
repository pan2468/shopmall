## 📌 쇼핑몰 프로젝트
스프링 부트 쇼핑몰 프로젝트 with JPA - 저자 변구훈 책을 읽고 클린코딩을 하여, 프로젝트 설정과 쇼핑몰 프로젝트의 도메인 구조 또는 구현과정에 대해서 알수 있었고
연관 관계 Entity들끼리 메인화면, 상품관리, 장바구니, 구매이력 등 매핑하여 조인에 대해서도 알수 있었습니다. 

### 👉 기능 설명
+ JpaRepository 인터페이스 CRUD 메소드 이용하여 상품관리, 구매이력, 장바구니 기능 구현
+ QueryDSL 객체지향 쿼리를 이용하여 검색조건 구현
+ SpringSecurity 설정
+ UserDetailsService 로그인 인증 구현

### 👉 제작기간, 참여인원
+ 제작기간: 2022.05.10 ~ 2022.05.15
+ 참여인원: 개인프로젝트
### 🛠 사용기술 (기술스택)
+ Java 11
+ SpringBoot 2.7.0
+ Spring Security
+ Spring Data JPA
+ QueryDSL 5.0.0
+ Maven
+ MySQL

## 👉 시퀀스 다이어그램

<img src="https://user-images.githubusercontent.com/58936137/180211415-6fb8869f-1fe0-4dc6-98fb-e76c55b335bf.png" width="800px" height="450px">


## 👉 서비스 화면

### 🎞 로그인 및 회원가입

<img src="https://user-images.githubusercontent.com/58936137/182033639-565713b2-9ffb-4d15-a7c9-3f7b85991fe5.gif" width="500px" height="300px">

### 🎞 상품 등록

<img src="https://user-images.githubusercontent.com/58936137/182033941-4ab87eb4-c0d0-402e-9fea-a753c1d7a92e.gif" width="500px" height="300px">



## 👉 핵심 기능

<details>
<summary><b>QueryDSL 설정</b></summary>
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

#### QueryDSL 세팅
	
+ Ctrl + Alt + Shift + S -> Modules -> Sources -> generated-sources 클릭
	
<img src="https://user-images.githubusercontent.com/58936137/180259777-92bd337c-d209-48a3-a7f2-53c19c90bdda.png" width="700px" height="500px">
	
</div>
</details>


<details>
<summary><b>QueryDSL 객체지향 쿼리</b></summary>
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
<summary><b>연관 관계 매핑</b></summary>
<div markdown="2">

### 연관 관계 일대일
+ @Column(name = "member_id")와 @JoinColumn(name = "member_id") 매핑합니다.
+ @OneToOne(fetch = FetchType.LAZY) 지연 로딩을 통해서 원하는 값만 출력
	
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

### 연관 관계 다대일 
+  @ManyToOne(fetch = FetchType.LAZY) 지연로딩 통해서 여러 Entity와 조인하여 출력
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

    private LocalDateTime orderDate; //주문일

    @Enumerated(EnumType.STRING)
    private OrderStatus orderStatus; //주문상태

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



   



