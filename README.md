# quiZdroidscript
Para adaptar a DS . Es un diseño de Quiz


// quiz from forum DS ... thanks to 0Symbroson Development
//Her is an example how I would do. Just take this as inspiration ;)
btns=['']
siz=0.4
questions=["Question1;Answer1;Answer2;Answer3;Answer4;3",
"Question2;Answer1;Answer2;Answer3;Answer4;1",
"Question3;Answer1;Answer2;Answer3;Answer4;4",
"Question4;Answer1;Answer2;Answer3;Answer4;2"]

function OnStart() {
        app.SetOrientation( "Portrait" );
        
        lay = app.CreateLayout( "Linear","FillXY,VCenter,HCenter" );
        lay.SetVisibility( "Hide" );
                question= app.CreateText( '',1,0.2 );
                question.SetTextSize( 20 );
                lay.AddChild( question );
                
                layAnswer= app.CreateLayout( "Absolute" );
                        addButton(0,0)
                        addButton(siz,0)
                        addButton(0,siz)
                        addButton(siz,siz)
                lay.AddChild( layAnswer );
        app.AddLayout( lay );
        
        nextQuestion();
}

function addButton(x,y) {
        var btn= app.CreateButton( '',siz-0.01,(siz-0.01)/2,"Custom" );
        btn.SetTextColor("black");
        btn.SetPosition( x,y/2 );
        btn.SetOnTouch( checkAnswer );
        layAnswer.AddChild( btn );
        btns.push(btn);
}

function nextQuestion() {
        quest= questions[ranInt(questions.length)].split(';')
        question.SetText( quest[0] );
        for( var i=1; i!=5; i++ ) {
                btns[i].SetText(quest[i])
                btns[i].SetStyle( "#ff8000","yellow",10 );
        }
        lay.Animate( "FadeIn",null,500 )
        layAnswer.SetTouchable( true );
}

function ranInt(v) {return Math.floor(Math.random()*v)}

function checkAnswer() {
        layAnswer.SetTouchable( false );
        if(quest.indexOf(this.GetText()) == quest[5] ) this.SetStyle("green")
        else this.SetStyle("red")
        setTimeout(questionOut,1000)
}
function questionOut() {lay.Animate( "FadeOut",nextQuestion,500 )}

// Don t know where to insert this code

//You can use a counter to count how many questions were asked and //asked correctly. To check a question was asked before you can set //the question string to null.
//example:
//questions=[q1;a1;a2;a3;r.a]
//count=0

function nextQuestion() {
    do
        a=questions[ranInt(questions.length)]
    while(!a)
    ask(a)
}

function ask(question){
    //show question
    count++
    questions[i]=null;
}

function checkAnswer() {
    //check right button pressed
    if(count==20) endSession();
    else nextQuestion();
}

//dont forget to set count 0 in endSession!

//hope the code helps you ;)
