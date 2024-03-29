# Smart Guide
* 스마트 가이드란 객체들을 움직일 때 다른 객체와의 정렬, 간격등을 고려하여 가이드 라인을 제시해 주고 가이드 라인에서는 고정시켜주는(snap) 기능을 말한다.
* 개체의 수가 많아질 경우 성능에 직접적으로 영향을 끼치기에 자료구조와, 알고리즘 쪽 조사가 필요함
* 다른 객체와의 정렬의 경우 IntervalTree 자료구조를 이용하여 겹치는 객체들의 x or y 좌표를 구해낼 수 있다. O(logN)
* 등간격의 경우 일반적으로 객체를 move, resize 시 삽입된 모든 개체에 대해서 탐색을 하고 현재 개체와의 거리를 구해야 하기에 일반적으로 O(N^2)의 시간 복잡도가 나오리라 예상
  * 대상 객체들이 각각 자신과 다른 객체들과의 간격 정보를 저장하도록 만든 뒤 해당 객체를 가로 혹은 세로 범위를 기준으로 다시 IntervalTree에 집어 넣음
  * Interval Tree를 이용하여 실시간으로 계속 검색하 되 대상 객체 식별 이후에는 계산되었던 간격 정보를 이용하여 빠르게 가이드라인을 표시해줌
## Interval tree 
* 간격 트리라고 불리며, key로 값이 아닌 구간을 가지는 것이 특징이다.
  * [1, 2] : value
  * 같은 범위를 가진 데이터가 여러개일 경우 모두 리턴이 가능하다.
```
example
import IntervalTree from '@flatten-js/interval-tree'

const tree = new IntervalTree();
const intervals = [[1, 10], [2, 10], [3, 7], [4, 7], [2, 8]];

for (let i = 0; i < intervals.length; i += 1) {
  tree.insert(intervals[i], `value${i}`)
}

const values = tree.search([5, 6]) => [val0 val1, val2, val3, val4]
```

## KonvaJS
* HTML5 2D context를 확장한 Canvas JavaScript FrameWork이다.
* Stage -> Layer -> Group -> Shape의 구조를 가진다.
* Stage 안에 각 Layer를 가지고, 그안에 group or shape를 가지는 구조이다.
#### Stage
* 화면상에 보이는 canvas 크기 및 동작 하는 행동들을 관리한다.
* event를 등록하여서 사용하는 곳
#### Layer
* Stage 공간 내에서 지정된 곳에서 Shape, Group이 그려지는 곳
#### Shape
* Layer 공간에 인스턴스 단위로 그려지는 모양
#### Group
* Layer 공간에 Shape를 하나로 묶어둔 형태이다.
