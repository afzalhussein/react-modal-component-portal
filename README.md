# react-modal-component-portal
React Portals provide a way to render children components into a DOM node that exists outside the DOM hierarchy of the parent component. This allows you to render content at a different place in the DOM, which can be useful for various scenarios, such as modals, tooltips, popovers, and more.

Here's an example illustrating the use of React Portals to create a modal dialog:

Let's create a Modal component that uses portals to render its content outside the regular component hierarchy:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';

const modalRoot = document.getElementById('modal-root');

class Modal extends React.Component {
  constructor(props) {
    super(props);
    this.el = document.createElement('div');
  }

  componentDidMount() {
    modalRoot.appendChild(this.el);
  }

  componentWillUnmount() {
    modalRoot.removeChild(this.el);
  }

  render() {
    return ReactDOM.createPortal(
      this.props.children,
      this.el,
    );
  }
}

export default Modal;
```

Now, let's use the Modal component in another part of your application:

```javascript
import React, { useState } from 'react';
import Modal from './Modal';

const App = () => {
  const [showModal, setShowModal] = useState(false);

  const toggleModal = () => {
    setShowModal(!showModal);
  };

  return (
    <div>
      <h1>React Portal Modal Example</h1>
      <button onClick={toggleModal}>Toggle Modal</button>
      {showModal && (
        <Modal>
          <div className="modal">
            <div className="modal-content">
              <h2>Modal Title</h2>
              <p>This is the modal content.</p>
              <button onClick={toggleModal}>Close Modal</button>
            </div>
          </div>
        </Modal>
      )}
    </div>
  );
};

export default App;
```

In this example:

- The `Modal` component is responsible for creating a portal outside the normal React component tree. It appends and removes a DOM node (`this.el`) from the `modal-root` element in the HTML document. The content passed to `Modal` via `props.children` will be rendered inside this portal.

- `App` component uses the `Modal` component and toggles the visibility of the modal with a button. When the modal is rendered, its content (a simple `div` with a close button in this case) is rendered within the portal and displayed as a modal dialog.

This example demonstrates how React Portals allow you to render content outside the normal DOM hierarchy, enabling the creation of UI elements like modals that are detached from their parent components and can be positioned anywhere in the DOM.
