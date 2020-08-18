---
layout: post
title:      "React Components"
date:       2020-08-16 20:24:54 -0400
permalink:  react_components
---


React components are modular, reusable bits of code. There are two types of components, class and functional components. These two components differ not only in their boilerplate, but also have different use cases. Class components extend the Component class, which allows the component to have state, utilize lifecycle methods, and contains a render method. In contrast, functional components are stateless, cannot utilize lifecycle methods, and do not contain a render method. Functional components are favored when changes in state are not needed to keep the component

Class Component:

```
class AttemptItem extends Component {

    state = {
        upVote: 0,
        downVote: 0
    }


//upvote button
    handleUpVote = () => {
        this.setState(prevState => ({
            upVote: prevState.upVote +1
        })
        )
    }

    handleDownVote = () => {
        this.setState(prevState => ({
            upVote: prevState.downVote -1
        })
        )
    }

    render(){
        const {content, diagram, timeStamp, attemptId, attempt_number} = this.props
        return(
            <div>
                <p>

                    {timeStamp}
                    <br/>
                    Attempt: #{attempt_number}
                     <br />
                     <Link className="attempt-content" to={`/attempts/${attemptId}/comments`}>
                    {content}
                    <br />
                    </Link>
                    <img src={diagram} alt="" height="350" width="300"/>
                    <br />
                    <button onClick={this.handleUpVote}>
                        Up Vote
                    </button>
                    {this.state.upVote}

                    <button onClick={this.handleDownVote}>
                        Down Vote
                    </button>
                    {this.state.downVote}
                    {/* <CommentForm/> */}
                </p>
            </div>
        )
    }  
}


export default AttemptItem

```

Functional Component:

```
