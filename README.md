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


## 💡 서비스 화면
 

### ✔ 회원 가입

<img src="https://user-images.githubusercontent.com/58936137/180049754-499d18ee-37ec-4c2b-91a3-3c869f5b1cd1.png" width="500px" height="300px">

<details>
<summary><b>개선 코드</b></summary>
<div markdown="2">

#### MemberController.class
~~~
    @PostMapping(value = "/new")
    public String newMember(@Valid MemberFormDto memberFormDto,
                            BindingResult bindingResult, Model model){
        if(bindingResult.hasErrors()){
            return "member/memberForm";
        }

        try{
            Member member = Member.createMember(memberFormDto,passwordEncoder);
            memberService.saveMember(member);
        }catch (IllegalStateException e){
            model.addAttribute("errorMessage",e.getMessage());
            return "member/memberForm";
        }
        return "redirect:/";
    }
~~~

#### MemberService.class

~~~
   public Member saveMember(Member member){
        validateDuplicateMember(member);
        return memberRepository.save(member);
    }
~~~

+ 이름, 이메일 주소, 비밀번호, 주소를 입력합니다.
+ JpaRepository 인터페이스 save() 메소드를 이용하여 등록하여 INSERT 삽입합니다. 
</div>
</details>


### ✔ 로그인하기 

<img src="https://user-images.githubusercontent.com/58936137/180049925-15194daf-d78d-4402-a48c-30da56db3bb3.png" width="500px" height="300px">

<details>
<summary><b>개선 코드</b></summary>
<div markdown="2">

#### MemberService.class
~~~
@Override
public UserDetails loadUserByUsername(String email) throws UsernameNotFoundException {
	Member member = memberRepository.findByEmail(email);

        if(member == null){
            throw new UsernameNotFoundException(email);
        }

        return User.builder()
                .username(member.getEmail())
                .password(member.getPassword())
                .roles(member.getRole().toString())
                .build();
    }
~~~


+ SpringSecurity 보안프레임워크에서 UserDetailsService 사용하여 로그인 인증
+ loadUserByUsername 메소드 매개변수 email 값을 받아 인증 확인

</div>
</details>


### ✔ Spring Security 설정

#### SecurityConfig.class
~~~

    @Override
    protected void configure(HttpSecurity http) throws Exception{
        http.formLogin()
                .loginPage("/members/login")
                .defaultSuccessUrl("/")
                .usernameParameter("email")
                .failureUrl("/members/login/error")
                .and()
                .logout()
                .logoutRequestMatcher(new AntPathRequestMatcher("/members/logout"))
                .logoutSuccessUrl("/");

        http.authorizeRequests()
                .mvcMatchers("/","/members/**",
                                    "/item/**","images/**").permitAll()
                .mvcMatchers("/admin/**").hasRole("ADMIN")
                .anyRequest().authenticated();

        http.exceptionHandling()
                .authenticationEntryPoint(new CustomAuthenticationEntryPoint());
    }
~~~


+ 로그인 접속시도 > email 값을 받아 인증 성공하면 .defaultSuccessUrl("/") 관리자 메인 페이지로 이동
+ 로그아웃 > .logoutSuccessUrl("/") 메인 페이지 이동




### ✔ 메인페이지

<img src="https://user-images.githubusercontent.com/58936137/180047764-3856a741-86e4-4f15-8344-eb117458f4d7.png" width="500px" height="300px">
	
+ 로그인 인증 성공시 redirect:/ 메인 페이지로 이동
+ ADMIN 로그인 시도 > 상품등록, 상품관리 메뉴가 링크 호출


### ✔ 상품 등록

<img src="https://user-images.githubusercontent.com/58936137/180048894-e95a367c-3537-4a1f-a2f8-1072f855e446.png" width="500px" height="300px">

<details>
<summary><b>개선 코드</b></summary>
<div markdown="2">

#### ItemService.class
~~~
	   public Long saveItem(ItemFormDto itemFormDto, List<MultipartFile> itemImgFileList) throws Exception {

        //상품 등록
        Item item = itemFormDto.createItem();
        itemRepository.save(item);

        //이미지 등록
        for(int i=0; i<itemImgFileList.size(); i++){
            ItemImg itemImg = new ItemImg();
            itemImg.setItem(item);
            if(i == 0)
                itemImg.setRepimgYn("Y");
            else
                itemImg.setRepimgYn("N");
            itemImgService.saveItemImg(itemImg, itemImgFileList.get(i));
        }
        return item.getId();
    }

~~~
	
+ JpaRepository 인터페이스 save() 메소드 이용해서 상품명, 가격, 재고, 상품 상세내용, 이미지 파일 저장 
	
</div>
</details>


### ✔ 상품 관리

<img src="https://user-images.githubusercontent.com/58936137/180050285-f3118855-a7df-4b9d-8dd5-f0ea1a90e2e6.png" width="500px" height="300px">

<details>
<summary><b>개선 코드</b></summary>
<div markdown="2">

#### ItemService.class
~~~
    @Transactional(readOnly = true)
    public Page<Item> getAdminItemPage(ItemSearchDto itemSearchDto, Pageable pageable){
        return itemRepository.getAdminItemPage(itemSearchDto,pageable);
    }
~~~

#### ItemRepositoryCustom
~~~
    Page<Item> getAdminItemPage(ItemSearchDto itemSearchDto, Pageable pageable);
~~~

+ JpaRepository 인터페이스 findAll() 메소드를 이용하여 공지사항에 상품 조회 출력

</div>
</details>


### ✔ 장바구니

<img src="https://user-images.githubusercontent.com/58936137/180050505-1fe08553-d81e-490b-a2bb-14cbf32389b0.png" width="500px" height="300px">

<details>
<summary><b>개선 코드</b></summary>
<div markdown="2">

#### CartController.class
~~~
    @GetMapping(value = "/cart")
    public String orderHist(Principal principal, Model model){
        List<CartDetailDto> cartDetailList = cartService.getCartList(principal.getName());
        model.addAttribute("cartItems",cartDetailList);
        return "cart/cartList";
    }
~~~

#### CartService.class
~~~
cartDetailDtoList = cartItemRepository.findCartDetailDtoList(cart.getId());
~~~

#### CartItemRepository.class
~~~
 @Query("select new com.shop.dto.CartDetailDto(ci.id, i.itemNm, i.price, ci.count, im.imgUrl)from CartItem ci, ItemImg im join ci.item i where ci.cart.id = :cartId and im.item.id = ci.item.id and im.repimgYn = 'Y' order by ci.regTime desc")
    List<CartDetailDto> findCartDetailDtoList(Long cartId);
~~~

+ 메인 페이지 상품 상세화면에서 장바구니 담기 버튼 클릭
+ cartItemRepository.findCartDetailDtoList(cart.getId()); 메소드 이용하여 장바구니 목록 출력 

</div>
</details>

### ✔ 주문하기

<img src="https://user-images.githubusercontent.com/58936137/180050705-1e926b70-604b-4ddb-b2a4-a52d976b2a12.png" width="500px" height="300px">

+ 장바구니 메뉴에서 주문하기 클릭 > 구매이력 findById() 상세출력    






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
<summary><b> findAll() 메소드의 복잡한 쿼리를 QueryDSL 이용하여 개선</b></summary>
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



   



