(async () => {
  // Ensure ExcalidrawAutomate is loaded
  if (!window.ExcalidrawAutomate) {
    new Notice("Excalidraw Automate is not loaded");
    return;
  }

  const ea = window.ExcalidrawAutomate;

  // Set the active view
  const views = app.workspace.getLeavesOfType('excalidraw');
  if (views.length === 0) {
    new Notice("No active Excalidraw view found");
    return;
  }
  const view = views[0].view;
  ea.setView(view);

  // Get all elements in the current view
  const elements = ea.getExcalidrawAPI().getSceneElements();

  // Unlock all elements
  elements.forEach(element => {
    element.locked = false;
  });

  // Apply the changes to the elements
  ea.getExcalidrawAPI().updateScene({ elements });
})();