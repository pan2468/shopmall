## 📌 쇼핑몰 프로젝트
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

## 👉 프로세스 화면

<details>
<summary><b>쇼핑몰 사용 메뉴얼</b></summary>
<div markdown="1">

<details>
<summary><b>로그인</b></summary>
<div markdown="2">
	
<img src="https://user-images.githubusercontent.com/58936137/180049925-15194daf-d78d-4402-a48c-30da56db3bb3.png" width="750px" height="450px">

### 로그인 인증
+ email, password 입력을 합니다.
+ SpringSecurity 보안프레임워크에서 UserDetailsService 사용하여 로그인 인증
</div>
</details>

<details>
<summary><b>회원 가입</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180049754-499d18ee-37ec-4c2b-91a3-3c869f5b1cd1.png" width="750px" height="450px">

### 회원가입 insert
+ 이름, 이메일 주소, 비밀번호, 주소를 입력합니다.
+ JpaRepository 인터페이스 save() 메소드를 이용하여 등록하여 INSERT 삽입합니다. 

</div>
</details>

<details>
<summary><b>메인 페이지</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180047764-3856a741-86e4-4f15-8344-eb117458f4d7.png" width="750px" height="450px">
	
### 메인페이지 
+ 로그인 인증 성공시 redirect:/ 메인 페이지로 이동합니다.
+ admin 로그인시 상품등록, 상품관리 메뉴가 링크 호출이 됩니다. 
</div>
</details>

<details>
<summary><b>상품 등록</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180048894-e95a367c-3537-4a1f-a2f8-1072f855e446.png" width="750px" height="450px">
	
### 상품 INSERT
+ JpaRepository 인터페이스 save()메소드 이용해서 상품명, 가격, 재고, 상품 상세내용, 이미지 파일을 삽입합니다. 
</div>
</details>

<details>
<summary><b>상품 관리</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180050285-f3118855-a7df-4b9d-8dd5-f0ea1a90e2e6.png" width="750px" height="450px">
	
### 상품 관리 목록 출력
+ JpaRepository 인터페이스 findAll() 메소드를 이용하여 공지사항에 상품 조회 출력
</div>
</details>

<details>
<summary><b>장바구니</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180050505-1fe08553-d81e-490b-a2bb-14cbf32389b0.png" width="750px" height="450px">
	
### 장바구니
+ 메인 페이지 상품 상세화면에서 장바구니 담기 버튼 클릭
+ JpaRepository save() 메소드 이용하여 장바구니 목록 출력 
</div>
</details>

<details>
<summary><b>구매이력</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180050705-1e926b70-604b-4ddb-b2a4-a52d976b2a12.png" width="750px" height="450px">
	
### 구매이력
+ 장바구니 화면에서 체크박스 클릭 후 주문하기 버튼 클릭 
+ JpaRepository save() 메소드 이용하여 구매이력 목록 출력 
</div>
</details>

</div>
</details>

## 👉 핵심 기능
<details>
<summary><b>QueryDSL 객체지향 쿼리</b></summary>
<div markdown="2">
	
~~~


import com.querydsl.core.QueryResults;
import com.querydsl.core.types.dsl.BooleanExpression;
import com.querydsl.jpa.impl.JPAQueryFactory;
import com.shop.constant.ItemSellStatus;
import com.shop.dto.ItemSearchDto;
import com.shop.dto.MainItemDto;
import com.shop.dto.QMainItemDto;
import com.shop.entity.Item;
import com.shop.entity.QItem;
import com.shop.entity.QItemImg;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.PageImpl;
import org.springframework.data.domain.Pageable;
import org.thymeleaf.util.StringUtils;

import javax.persistence.EntityManager;
import java.time.LocalDateTime;
import java.util.List;

public class ItemRepositoryCustomImpl implements ItemRepositoryCustom{

    private JPAQueryFactory queryFactory;

    public ItemRepositoryCustomImpl(EntityManager em){
        this.queryFactory = new JPAQueryFactory(em);
    }

    private BooleanExpression searchSellStatusEq(ItemSellStatus searchSellStatus){
        return searchSellStatus == null ? null : QItem.item.itemSellStatus.eq(searchSellStatus);
    }

    private BooleanExpression regDtsAfter(String searchDateType){
        LocalDateTime dateTime = LocalDateTime.now();

        if(StringUtils.equals("all",searchDateType) || searchDateType == null){
            return null;
        }else if(StringUtils.equals("1d", searchDateType)){
            dateTime = dateTime.minusDays(1);
        }else if(StringUtils.equals("1w", searchDateType)){
            dateTime = dateTime.minusWeeks(1);
        }else if(StringUtils.equals("1m", searchDateType)){
            dateTime = dateTime.minusMonths(1);
        }else if(StringUtils.equals("6m",searchDateType)){
            dateTime = dateTime.minusMonths(6);
        }
        return QItem.item.regTime.after(dateTime);
    }

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

    private BooleanExpression itemNmLike(String searchQuery){
        return StringUtils.isEmpty(searchQuery) ?
                null : QItem.item.itemNm.like("%" + searchQuery + "%");
    }


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


## 👉 핵심 트러블슈팅 경험 
   



