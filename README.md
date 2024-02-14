import React, { useState, useEffect } from 'react';
import axios from 'axios';
import Loader from 'react-spinners/ClipLoader'; // Example of using React Spinners library

const YourComponent = () => {
  const [isLoading, setIsLoading] = useState(true);
  const [listItems, setListItems] = useState([]);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await axios.get('List Creation API URL');
        setListItems(response.data); // Assuming the response contains list items
        setIsLoading(false);
      } catch (error) {
        setError(error);
        setIsLoading(false);
      }
    };

    fetchData();
  }, []);

  return (
    <div>
      {isLoading ? (
        <Loader size={50} color={"#123abc"} loading={isLoading} /> // Example of using React Spinners
      ) : error ? (
        <FailureView />
      ) : (
        <YourListComponent listItems={listItems} />
      )}
    </div>
  );
};

const FailureView = () => (
  <div>
    <img src="https://assets.ccbp.in/frontend/content/react-js/list-creation-failure-lg-output.png" alt="Failure View" />
    <p>Failed to fetch data. Please try again.</p>
    <button onClick={() => window.location.reload()}>Try Again</button>
  </div>
);

const YourListComponent = ({ listItems }) => (
  <div>
    {/* Render your list items based on the received data */}
  </div>
);

export default YourComponent;
