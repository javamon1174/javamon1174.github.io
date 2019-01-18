---
title: "[파이썬 웹 프로그래밍] 첫 번째 장고 앱 작성하기, part 4 - 함수 뷰 처리에서 제네릭뷰 처리로"
excerpt: "장고 앱 작성하기"
date: 2019-01-20
categories:
  - python
  - tech
  - django
tags:
  - python
  - django
  - generic
---
해당 교재를 처음 읽어 나갈 때 해당 과제를 스킵하고 지나갔었다.
하지만 두번째 회독하면서 해당 과제를 해결하고 지나가는게 맞다고 생각되었다.

따로 실습이나 과제라고 명시되어 있지는 않지만 책 내용에선 이렇게 언급되고 있다.
"vote() 뷰 함수도 제네릭 뷰로 변경할 수 있습니다..(중략) 스스로 시도 해보는 것이 좋은 공부가 될 것입니다."

그래서 약 30분의 시간을 소모하면서 vote() 뷰 함수를 제네릭 뷰로 바꾸고 테스트도 진행하니 잘 되었다!

장고 공홈에는 폼 처리에 대해 사용자가 정의한 폼을 활용해서 다루는 방식만 있기 때문에 내가 원하는 작업에 대한 내용은 없었다.

관련 내용 : https://docs.djangoproject.com/ko/2.1/intro/tutorial04/

문제 :
views.py 파일의 vote() 함수를 generic view(클래스형 뷰)로 대체

해결 방법 :
책의 클래스형 뷰의 개념 내용을 참고하여 구현

과정 :
1. 먼저 클래스형 뷰에서는 인수를 pk로 받기 때문에 urls.py 의 vote url 패턴의 인수명을 pk로 변경하고 두번째 인자로 VoteView 클래스 명으로 변경 하였다.

```python
# polls/urls.py

path('<int:question_id>/vote/', views.vote, name='vote'),
```
위의 코드를 아래 코드로 바꾸었다.
```python
# polls/urls.py

path('<int:pk>/vote/', views.VoteView.as_view(), name='vote'),
```
2. vote()의 함수를 제네릭 뷰로 대체하였다.

=> 이 순간 의문점이 들었다 일반 제네릭 뷰를 사용해야 할지 업데이트 뷰를 사용해야 할지, 결론부터 말하면

오버라이딩으로 둘다 같은 동작하기때문에 아무거나 사용해도 되지만, 실제 사용자 정의 폼을 다루고 업데이트뷰의 역할만 필요하다면 업데이트뷰를 사용하는 것이 맞다고 생각한다.

```python
# polls/views.py

def vote(request, question_id):
    logger.debug("vote().question_id : %s" % question_id) # logging test
    question = get_object_or_404(Question, pk=question_id)
    try :
        selected_choice = question.choice_set.get(pk=request.POST['choice'])

    except (KeyError, Choice.DoesNotExist) :
        return render(request, 'polls/detail.html', {
            'question': question,
            'error_message': 'You didn\'t select a choice'
        })

    else :
        selected_choice.votes += 1
        selected_choice.save()
        return HttpResponseRedirect(reverse('polls:results', args=(question_id,)))
```
위의 코드는 참고사이트와 책에도 같은 내용으로 있는 코드이다.
위의 POST 처리를 제네릭뷰로 대체하였다. 

```python
# polls/view.py

class VoteView(View) :
    def post(self, request, pk):
        logger.debug("vote().question_id : %s" % pk)  # logging test
        question = get_object_or_404(Question, pk=pk)

        try:
            selected_choice = question.choice_set.get(pk=request.POST['choice'])

        except (KeyError, Choice.DoesNotExist):
            return render(request, 'polls/detail.html', {
                'question': question,
                'error_message': 'You didn\'t select a choice'
            })

        else:
            selected_choice.votes += 1
            selected_choice.save()
            return HttpResponseRedirect(reverse('polls:results', args=(pk,)))
```
post 메소드를 오버라이딩하고 인수로 url패턴에 있던 변수명 pk를 추가하여 기존의 question_id 의 변수를 대체하였다.
